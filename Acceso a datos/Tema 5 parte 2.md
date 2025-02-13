```
db.products.insertMany([
  {
    "codigo": "B67890",
    "denominacion": "Auriculares Inalámbricos",
    "pvp": 49.99,
    "categoria": "Accesorios",
    "uv": 5,
    "stock": 100
  },
  {
    "codigo": "C23456",
    "denominacion": "Smartphone Modelo X",
    "pvp": 299.99,
    "categoria": "Electrónica",
    "uv": 15,
    "stock": 30
  }
]);

[{
  $project: {
    artículo: { $toUpper: "$denominación" }, 
    importe: { $multiply: ["$pvp", "$uv"] },
		stockactual: { $subtract: ["$stock", "$uv"] },
    areponer: {
			$cond: [{$lte: [{ $subtract: ["$stock", "$uv"] }, 0]}, true, false] }
  }
}
]
[{
 $group: {
   _id: "$categoria",
   contador: {$sum: 1},
   sumaunidades: { $sum: "$uv"},
   totalimporte: {$sum: {$multiply: ["$pvp", "$uv"]}}
 } 
}]
```

```
[
  {
    $project: {
      nombre: "$nombre.nomb",
      numerooficios: {
        $size: { $ifNull: ["$oficios", []] }
      },
      numeroprimas: {
        $size: { $ifNull: ["$primas", []] }
      },
      oficiosconcatenados: {
        $concatArrays: ["$oficios", "$primas"]
      }
    }
  }
]
```

```
[
  { $sort: { "direccion.población": 1 } },
  {
    $project: {
      poblacion: "$direccion.poblacion",
      nombre: "$nombre.nomb",
      ape1: "$nombre.ape1",
      ape2: "$nombre.ape2",
      oficio1: { $arrayElemAt: ["$oficios", 0] },
      oficio2: { $arrayElemAt: ["$oficios", 1] },
      oficioultimo: {
        $arrayElemAt: ["$oficios", -1]
      }
    }
  }
]
```

```
departrabajo = db.depart.findOne({_id: 'dep1'})
```

```
db.emple.find({_id: { $in : departrabajo.emple } } )
```

```
emplesdep = db.emple.find({_id: { $in: 
```

```
departrabajo.emple } }).toArray()
```

```
departrabajo = db.depart.findOne({_id: 'dep2'})
```

```
emplesdep = db.emple.find({_id: { $in: departrabajo.emple }, salario: {$gt:1400 }} ).toArray()
```

