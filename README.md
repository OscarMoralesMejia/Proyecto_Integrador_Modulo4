# Proyecto_Integrador_Modulo4
Proyecto donde se muestra la puesta en marcha de un entorno Big Data<br>
1.- HDFS<br>
Primero montamos la imagen de NameNode de Hadoop en un servidor Linux Ubuntu
lo que podemos ver en las siguientes imagenes:<br>
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/3726fcd7-18e2-4d10-80e6-3b315c607469)
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/d1eba69a-e912-4eb4-a5ab-25e574af7b83)
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
