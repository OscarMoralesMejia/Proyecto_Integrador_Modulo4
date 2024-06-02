# Módulo Hive
Objetivo.- Levantar un contenedor Hive y crear una base de datos con algunas tablas a partir de archivos ingestados en HDFS.

Solución: 

#### Paso 1.-Correr docker-compose de Hive
Para poder levantar el contenedor de Hive nos apoyamos del archivo docker-compose-v2.yml el cuál contiene las imagenes necesarias para levantar el servicio de Hive, para esto ejecutamos el siguiente comando desde la consola de putty

```
sudo docker-compose -f docker-compose-v2.yml up -d
 ```
#### Paso 2.-Copiamos script de BD
Para poder generar la bd y las tablas necesarias copiamos el script con el siguiente comando desde el path /home/ubuntu/herramientas_big_data

```
sudo docker cp Paso02.hql hive-server:/opt/hive/scripts/Paso02.hql
```
#### Paso 3.- Ejecutar script
Entramos al contenedor de hive y ejecutamos el siguiente comando
```
sudo docker exec -it hive-server bash
```
ya dentro del contenedor de hive ejecutamos el siguiente comando
```
hive -f /opt/hive/scripts/Paso02.hql
```
y con esto logramos generar la base de datos con algunas tablas con datos proporcionados de los archivos que estan en la carpeta data de hdfs




