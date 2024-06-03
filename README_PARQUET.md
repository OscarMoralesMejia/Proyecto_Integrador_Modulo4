# Formatos de Almacenamiento
#### Paso 1.- Crear carpeta origen
Volvemos a crear una carpeta para copiar nuevamente los datos le llamaremos data2 y lo hacemos con los siguientes comandos:
a)Con la primer linea de comando entramos al contenedor namenode
b)Con la segunda línea de comando creamos el directorio data2
c)Con la tercer línea copiamos todo elcontenido de la carpeta Datasets2 que contiene los archivos parquet a la carpeta data2
```
sudo docker exec -it namenode bash
hdfs dfs -mkdir -p /data2
hdfs dfs -put /home/Datasets2/* /data2
```
#### Paso 2.- Correr Script Parquet
Para generar la base de datos en formato parquet se modifica el script de creación colocando en STORED AS PARQUET
el archivo es:Paso03.hql
Para esto entramos tenemos que ejecutar las siguientes lineas de comando:
a)con la primer línea copiamos el *script* de creación de base de datos que contiene la definición de las tablas con el formato parquet
b)Después entramos al contenedor hive-server
c)Con la tercer línea ejecutamos el script lo cual genera la base de datos integrador2
```
sudo docker cp Paso03.hql hive-server:/opt/hive/scripts/Paso03.hql
sudo docker exec -it hive-server bash
hive -f /opt/hive/scripts/Paso03.hql
```
En la siguiente imagen podemos constatar que se ha creado la base de datos integrador2
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/9e6f8af1-401e-41be-9386-56079cc2ecec)

y podemos ver las tablas y la descripcion de alguna tabla para checar el formato que sea parquet
```
use integrador2;
show tables;
describe formatted cliente;
```
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/6ecae7ee-d77d-407c-be05-3252281354cd)
<br>
Datos Parquet<br>
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/9750f6e5-6504-4500-915f-376185035e4a)
<br>
Datos scv<br>
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/24d6589b-d4dd-4463-9128-bf980cf94096)
