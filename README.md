# Módulo HDFS
Objetivo.- Levantar un contenedor hadoop para almacenar un set de datos proporcionados en formato csv <br>

Solución:
Para Cumplir con el objetivo hay que levantar un contenedor proporcionado en el archivo docker-compose-v1.yml, creamos una carpeta intermedia dentro del contenedor para despues estando dentro del contenedor usar el set de datos para integrarlos al sistema de archivos de hadoop.
Herramientas usadas:
a) maquina virtual con un servidor linux ubuntu y
b) Putty

## Pasos de la solución:
#### Paso 1.- Encender la maquina virtual que previo ya esta configurada para usarse en un sistema host windows
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/6519ac55-8b4a-4570-9612-f8eeb837e02b)

#### Paso 2.- Entrar al servidor linux mediante la consola de putty
Esto lo hacemos obteniendo la ip de nuestro servidor linux con el siguiente comando
```
namehost -I
```
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/83dcd62b-3ad9-4b78-b29a-e6e370c61cbb) <br>
La ip obtenida se coloca en putty para podernos conectar al servidor linux <br>
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/98c63a5c-9f75-4fdd-a386-64228b577060)<br>
Una vez conectados debemos ir al paso 3

#### Paso 3.-Clonar proyecto integrador
Podemos clonar el proyecto con el siguiente comando ejecutandolo en la terminal de putty.
```
git clone https://github.com/soyHenry/DS-M4-Herramientas_Big_Data.git
```  
Ya una vez que se clono el repositorio se tiene la carpeta herramientas_big_data a la cual accedemos con el comando:
```
cd herramientas_big_data
```  
y debemos de ver la siguiente pantalla , podemos ejecutar el comando ls para ver el contenido de dicha carpeta<br>  
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/8eb506b0-ff83-407f-bcb2-d1b10e0b423d)

#### Paso 4.-Ejecutar archivo docker-compose
Ejecutamos el archivo docker-compose para levantar el contenedor con la infraestructura hadoop con el siguiente comando ya que en el archivo docker-compose-v1.yml están la imagenes necesarias para levantar el servidor de nodo maestro los nodos esclavos datanodes asi como el servidor espejo.
```
sudo docker-compose -f docker-compose-v1.yml up -d
```
#### Paso 5.-Copiar datos a carpeta dentro del contenedor
Para copiar al contenedor los archivos de la carpeta Datasets primero accesamos al contenedor hadoop para crear dentro del contenedor una carpeta de igual nombre Datasets que será el destino de nuestros archivos fuente
``` 
sudo docker exec -it namenode bash
```
<br>
nos movemos al directorio home y creamos una carpeta con el nombre Datasets con el siguiente código<br>

```
cd home
mkdir Datasets
exit
```  
después nos salimos del contenedor de docker con el comando exit, por lo que regresamos al directorio de herramientas_big_data, recordando que con el comando pwd que significa print working directory podemos ver en que ruta estamos y poder lograr el copiado hacia la carpeta Datasets
```
sudo docker cp Datasets  namenode:/home
```    
#### Paso 6.-Crear directorio hdfs dentro del contenedor
Ahora necesitamos crear una carpeta que llamaremos *data* dentro del hdfs, para esto entramos al contenedor namenode y creamos la carpeta con los siguientes comandos:
```
sudo docker exec -it namenode bash
hdfs dfs -mkdir -p /data
```

Recordando que con el siguientes comandos podemos ver lo que hay dentro del sistema de archivos hdfs ya sea en raiz o en el directorio *data*

```
hdfs dfs -ls /
hdfs dfs -ls /data
```
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/53cc1449-2165-466f-a03c-857436f5e358)

Por último ejecutamos el siguiente comando, para copiar dentro del contenedor en el directorio *data* todos los archivos que estan dentro de la carpeta Datasets
```
hdfs dfs -put /home/Datasets/* /data
```
Existe otra forma de hacer lo anterior generando las instrucciones en un archivo con extensión .sh

#### Paso 7.- Checar contendedor
Podemos checar que el contenedor de hadoop este arriba, los valores de tamaño de bloque y factor de replica y que los archivos se hayan cargado en el directorio hdfs.
a) Para checar que este arriba el sistema de archivos hdfs podemos usar el explorador de internet con la siguiente url , se tiene que usar la ip de la maquina host(servidor linux ubuntu)
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/d1eba69a-e912-4eb4-a5ab-25e574af7b83)
b)para checar los valores de tamaño de bloque podemos usar algún explorador con la siguiente url en mi caso uso la ip de mi maquina virtual obteniendo lo siguiente en el explorador
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/3726fcd7-18e2-4d10-80e6-3b315c607469)
El bloque dfs.blocksize es el siguiente:
```xml
<property>
<name>ftp.blocksize</name>
<value>67108864</value>
<final>false</final>
<source>core-default.xml</source>
</property>
```
<br>
El dfs.replication es:

```xml
<property>
<name>dfs.replication</name>
<value>3</value>
<final>false</final>
<source>hdfs-default.xml</source>
</property>
```
c) Y para saber si estan cargados los archivos en el sistema hdfs  podemos entrar al contenedor y checar la ruta del la carpeta *data*
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/5573b2c0-fc43-4517-bad9-33c54c276304)
