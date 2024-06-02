# Formatos de Almacenamiento
#### Paso 1 Crear carpeta origen
Volvemos a crear una carpeta para copiar nuevamente los datos le llamaremos data2 y lo hacemos con los siguientes comandos
```
sudo docker exec -it namenode bash
hdfs dfs -mkdir -p /data2
hdfs dfs -put /home/Datasets/* /data2
```
#### Paso 2 Correr Script Parquet
Para generar la base de datos en formato parquet se modifica el script de creación colocando en FORMAT : Parquet
el archivo es:Paso03.hql
Para esto entramos al contenedor de hive
```
sudo docker cp Paso03.hql hive-server:/opt/hive/scripts/Paso03.hql
sudo docker exec -it hive-server bash
hive -f /opt/hive/scripts/Paso03.hql
```
Lo cual genera la base de datos integrador2
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/9e6f8af1-401e-41be-9386-56079cc2ecec)

y podemos ver las tablas y la descripcion de alguna tabla para checar el formato que sea parquet
```
use integrador2;

```
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/6ecae7ee-d77d-407c-be05-3252281354cd)
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/24d6589b-d4dd-4463-9128-bf980cf94096)
