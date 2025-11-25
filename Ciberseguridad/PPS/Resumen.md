## 1. Docker: conceptos + comandos imprescindibles

Conceptos clave:  
- Contenedor vs máquina virtual; imagen vs contenedor vs registro.
- Volúmenes (docker volume) vs bind mounts (-v /ruta_host:/ruta_contenedor).
- Redes: none, bridge, host, redes bridge personalizadas, macvlan; conexión entre contenedores.
- Dockerfile: FROM, RUN, ENV, EXPOSE, COPY/ADD, CMD/ENTRYPOINT.

Comandos que tienes que saber qué hacen:  
- Información y listado:  
  - docker help, docker version, docker images, docker ps, docker ps -a.
- Trabajo con imágenes:  
  - docker pull, docker rmi, docker inspect imagen, docker tag, docker save, docker load.
- Trabajo con contenedores:  
  - docker run [opciones] imagen: -d, -it, --name, -p host:cont, --network, -v/--mount.
  - docker stop, docker start, docker rm, docker rm -f $(docker ps -aq).
  - docker exec -it contenedor comando, docker attach, docker top, docker inspect contenedor.
- Volúmenes:  
  - docker volume create, docker volume ls, docker volume rm, docker run -v nombre:/ruta.
- Limpieza:  
  - docker system prune (-a), docker image prune, docker volume prune, docker network prune.

Comandos específicos de tus prácticas (muy preguntables):  
- MySQL: docker run -d -p 3306:3306 --name mysql-db1 -e MYSQL_ROOT_PASSWORD=… mysql:tag; acceso con docker exec -it mysql-db1 mysql -p.
- phpMyAdmin: docker run -d --rm --name phpmyadminc --link mysql-db1 -e PMA_HOST=mysql-db1 -p 9080:80 phpmyadmin/phpmyadmin.
- Docker Compose: docker-compose --version, docker-compose up (-d), docker-compose down.

## 2. Kubernetes: conceptos + comandos imprescindibles

Conceptos clave:  
- Orquestador: controla creación, estado y errores de contenedores en cluster.
- Pod: unidad mínima de despliegue, uno o varios contenedores que comparten red y almacenamiento.  
- Deployment: estado deseado (imagen, réplicas, estrategia de actualización) que usa ReplicaSets.  
- Service: IP estable para un conjunto de Pods; desacopla cliente/Pods.
- Ingress: entrada HTTP/HTTPS con reglas de host/ruta y TLS, apoyado en Services.
- Tipos de Service y puertos:  
  - ClusterIP (interno al cluster), NodePort (expuesto en nodos), LoadBalancer (LB externo), ExternalName, Headless (ClusterIP: None).  
  - targetPort = puerto del contenedor; port = puerto del service; nodePort = puerto en el nodo.

Comandos kubectl que debes reconocer:  
- Ver estado:  
  - kubectl cluster-info  
  - kubectl get nodes  
  - kubectl get pods --all-namespaces  
  - kubectl get deployments --all-namespaces  
  - kubectl get services
- Aplicar y borrar YAML:  
  - kubectl apply -f fichero.yaml  
  - kubectl delete -f fichero.yaml  
  - kubectl delete deployment nombre  
  - kubectl delete service nombre
- Inspeccionar recursos:  
  - kubectl describe pod nombre-pod  
  - kubectl describe deployment nombre
- Escalar: kubectl scale deployments/nombre --replicas=N.
- Debug/acceso:  
  - kubectl exec -it pod sh  
  - kubectl port-forward pod/nombre 8081:80 --address 0.0.0.0

Preguntas típicas de test:  
- “¿Qué recurso de Kubernetes expone una IP estable frente a un conjunto de Pods?” → Service.
- “¿Qué tipo de Service usas para exponer un puerto en todos los nodos?” → NodePort.

## 3. Vagrant y Ansible: entorno de laboratorio y configuración

Conceptos Vagrant:  
- Vagrant = herramienta para crear y configurar entornos de desarrollo virtualizados sobre VirtualBox, VMware, AWS, etc.
- Box = imagen base empaquetada; se gestionan con vagrant box add/list.
- Vagrantfile = archivo de configuración donde defines box, RAM, CPU, nombre, red, puertos, discos, provisioners (shell/ansible).
- Redes:  
  - private_network ip … (red privada 192.168.56.x).  
  - public_network, bridge eth0 (modo puente).  
  - forwarded_port guest:80 host:8080.

Comandos Vagrant:  
- vagrant box list, vagrant box add nombre, vagrant package --base MV --output caja.box.
- vagrant init (o vagrant init -m box), vagrant up, vagrant ssh, vagrant halt, vagrant destroy.
- vagrant status, vagrant reload, vagrant suspend, vagrant resume.
- vagrant snapshot save, vagrant snapshot restore, vagrant snapshot push/pop.
- vagrant ssh-config (para ver HostName, Port, IdentityFile) y usar ssh manual.
- vagrant plugin list, vagrant plugin install, plugins como vagrant-aws y vagrant-persistent-storage.

Provisioning en Vagrant:  
- Shell externo: config.vm.provision "shell", path "actualizar.sh".  
- Shell inline: config.vm.provision "shell", inline: <<-SHELL … SHELL.
- Ansible como provisioner: config.vm.provision "ansible" do |ansible| ansible.playbook = "site.yml" end.   

Conceptos Ansible:  
- Herramienta libre para configurar y administrar nodos por SSH; instala paquetes, crea usuarios, gestiona ficheros, etc.
- Componentes: inventario (hosts), playbooks (YAML), módulos (apt, file, service, copy, command, user), variables, handlers, roles.
- No requiere agente en los nodos, solo SSH y Python.

Comandos Ansible importantes:  
- ansible --version.  
- ansible all -m ping -u vagrant (ad-hoc).
- ansible-playbook -u vagrant -i hosts libro.yml.

Cosas típicas de playbooks:  
- Uso de become: become: yes para ejecutar como root.
- Módulo apt: state=latest / absent para instalar/desinstalar.  
- Módulo file: state=touch / directory / absent, mode, owner, group.  
- Módulo copy: copia ficheros, with_items para varios.  
- register + debug: guardar salida en variable y mostrarla (stdout vs stdout_lines).
- when: ejecutar tareas condicionalmente.
- handlers: tareas que se ejecutan cuando se notifica (notify) después de cambios (ej. reiniciar nginx).

## 4. Terraform y Proxmox: IaC “seria”

Conceptos Terraform esenciales:  
- Terraform = herramienta de HashiCorp para crear/gestionar infraestructura de forma declarativa (IaC).
- Características clave:  
  - Multiplataforma (AWS, Azure, GCP, VMware, Proxmox…).  
  - Estado de infraestructura (archivo de estado).  
  - Planificación previa (terraform plan) y aplicación controlada (terraform apply).  
  - Módulos reutilizables, paralelismo y escalabilidad.  
  - Integración con otras herramientas (Ansible, Puppet, etc.).

Estructura de proyecto Terraform:  
- main.tf: recursos principales y proveedores.  
- variables.tf: definición de variables.  
- outputs.tf: salidas (IPs, IDs).  
- provider.tf: configuración del provider.  
- backend.tf: backend de estado remoto/local.  
- data.tf: fuentes de datos.  
- terraform.tfvars: valores por defecto.  
- modules/ para módulos.

Comandos Terraform que deben sonarte:  
- terraform init: inicializar proyecto y descargar providers/módulos.  
- terraform plan: ver qué se va a crear/modificar/borrar.  
- terraform apply: aplicar cambios.  
- terraform destroy: destruir recursos.
- terraform validate: validar sintaxis.  
- terraform refresh: actualizar estado desde infra real.  
- terraform output: mostrar outputs.  
- terraform state …: gestionar el estado.  
- terraform import: importar recursos existentes.  
- terraform workspace: gestionar entornos (dev/prod).

Proxmox en la práctica:  
- Proxmox VE: plataforma de virtualización (KVM + LXC) con HA, snapshots, backups.
- Cloud-init: inicializa instancias (IP, usuario, clave SSH) al arranque, usado en plantillas Ubuntu cloud-image.
- Provider Proxmox (telmate/proxmox) en Terraform:  
  - provider "proxmox" { pm_api_url, pm_api_token_id, pm_api_token_secret, pm_tls_insecure} 
  - resource "proxmox_vm_qemu" para crear VMs con plantilla cloud-init, ipconfig0, cores, sockets, disks, bridge vmbr0, sshkeys.
- Flujo típico: crear plantilla Ubuntu cloud-init en Proxmox, configurar token usuario, luego usar terraform init/plan/apply para levantar VMs desde main.tf.