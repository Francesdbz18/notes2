```
/etc/yum.repos.d/mongodb-org-8.2.repo

[mongodb-org-8.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/8.2/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-8.0.asc
```
```
/usr/bin/mongodb-compass
/usr/bin/mongos
/usr/bin/mongod
/usr/bin/mongosh
/usr/bin/mongodump
/usr/bin/mongoexport
/usr/bin/mongofiles
/usr/bin/mongoimport
/usr/bin/mongorestore
/usr/bin/mongostat
/usr/bin/mongotop

```

## docker-compose.yml completo

```yaml
version: "3.8"

services:
  # CONFIG SERVER
  config:
    image: mongo
    container_name: config
    command: ["mongod", "--configsvr", "--replSet", "configReplSet", "--bind_ip_all"]
    ports:
      - "27018:27017"       # opcional, por si quieres entrar desde el host
    volumes:
      - configdata:/data/db
    networks:
      - red-mongo

  # SHARD 1
  shard1:
    image: mongo
    container_name: shard1
    command: ["mongod", "--shardsvr", "--replSet", "shard1rs", "--bind_ip_all"]
    ports:
      - "27019:27017"
    volumes:
      - shard1data:/data/db
    networks:
      - red-mongo
    depends_on:
      - config

  # SHARD 2
  shard2:
    image: mongo
    container_name: shard2
    command: ["mongod", "--shardsvr", "--replSet", "shard2rs", "--bind_ip_all"]
    ports:
      - "27020:27017"
    volumes:
      - shard2data:/data/db
    networks:
      - red-mongo
    depends_on:
      - config

  # ROUTER MONGOS
  mongos:
    image: mongo
    container_name: mongos
    command: [
      "mongos",
      "--configdb", "configReplSet/config:27017",
      "--bind_ip_all"
    ]
    ports:
      - "27017:27017"       # aquí te conectarás tú (mongosh, apps, etc.)
    depends_on:
      - config
      - shard1
      - shard2
    networks:
      - red-mongo

volumes:
  configdata:
  shard1data:
  shard2data:

networks:
  red-mongo:
```

Este compose refleja la arquitectura mínima: 1 config server, 2 shards y 1 mongos.[^3][^1]

***

## Pasos para levantar el clúster

1. Guardar el archivo como `docker-compose.yml` en un directorio.
2. Levantar todo:
```bash
docker compose up -d
```

Comprueba que los contenedores están “up”:

```bash
docker ps
```


***

## Inicializar config server y shards

MongoDB necesita que los replica sets estén inicializados aunque tengan un solo nodo.[^2][^4]

### 1) Inicializar el config server

```bash
docker exec -it config mongosh
```

Dentro de `mongosh`:

```js
rs.initiate({
  _id: "configReplSet",
  configsvr: true,
  members: [
    { _id: 0, host: "config:27017" }
  ]
})
```

Comprueba:

```js
rs.status()
```

Sal de `mongosh` con `exit`.

### 2) Inicializar shard1

```bash
docker exec -it shard1 mongosh
```

Dentro:

```js
rs.initiate({
  _id: "shard1rs",
  members: [
    { _id: 0, host: "shard1:27017" }
  ]
})
rs.status()
exit
```


### 3) Inicializar shard2

```bash
docker exec -it shard2 mongosh
```

Dentro:

```js
rs.initiate({
  _id: "shard2rs",
  members: [
    { _id: 0, host: "shard2:27017" }
  ]
})
rs.status()
exit
```


***

## Conectar a mongos y añadir los shards

Ahora todo se hace a través del router `mongos` (puerto 27017 del host).[^5][^1]

1. Conectarte:
```bash
mongosh "mongodb://localhost:27017"
```

2. Añadir los shards:
```js
sh.addShard("shard1rs/shard1:27017")
sh.addShard("shard2rs/shard2:27017")
sh.status()
```

Con esto ya tienes un clúster fragmentado con 2 shards y 1 config server.

***

## Activar sharding y cargar la colección cities

La práctica menciona usar la colección de ciudades (`cities.mongodb`) y la guía de DigitalOcean para elegir la clave de fragmentación.[^6][^7][^8]

### 1) Crear base de datos y colección

Desde `mongos` (ya conectado a `localhost:27017`):

```js
use ciudades
db.createCollection("cities")
```


### 2) Activar sharding en la base de datos

```js
sh.enableSharding("ciudades")
```


### 3) Elegir una clave de fragmentación

Por ejemplo, usar `continent` con `hashed` (bien para repartir uniformemente documentos pequeños como tus ciudades).[^8][^5]

```js
sh.shardCollection("ciudades.cities", { continent: "hashed" })
```


### 4) Importar el archivo `cities.mongodb`

En tu máquina host (en la carpeta donde tengas `cities.mongodb`):[^7][^6]

```bash
mongoimport \
  --uri "mongodb://localhost:27017/ciudades" \
  --file cities.mongodb \
  --jsonArray
```

Tu archivo ya es un `insertMany` pero `mongoimport` espera JSON; si lo tienes exactamente como en el adjunto (script JS), puedes en su lugar hacer:[^6]

```bash
mongosh "mongodb://localhost:27017/ciudades" cities.mongodb
```

Eso ejecutará el `insertMany` contra el router `mongos`, así los datos entran al clúster shardeado.[^8]

***

## Comprobar que realmente está fragmentando

Desde `mongos`:

```js
use ciudades
db.cities.find()
sh.status()
db.cities.getShardDistribution()
```

Verás en qué shard se han quedado los documentos y cómo están distribuidos los chunks.[^2][^5]

***

Si quieres, en el siguiente mensaje se puede pulir el compose para que lleve comentarios “bonitos” para entregar o adaptarlo exactamente a los nombres/puertos que use vuestro guion de clase.

<div align="center">⁂</div>

[^1]: https://phoenixnap.com/kb/mongodb-sharding

[^2]: https://www.geeksforgeeks.org/mongodb/setting-up-a-mongodb-sharded-cluster/

[^3]: https://stackoverflow.com/questions/5684993/is-this-the-optimal-minimum-setup-for-mongodb-to-allow-for-sharding-scaling

[^4]: https://www.mongodb.com/community/forums/t/sharding-configuration-server-mongos-mongosh/130016

[^5]: https://www.bmc.com/blogs/mongodb-sharding-explained/

[^6]: cities.mongodb

[^7]: Cluster-de-sharding-fragmentacion-en-MongoDB.pdf

[^8]: https://www.digitalocean.com/community/tutorials/how-to-use-sharding-in-mongodb
