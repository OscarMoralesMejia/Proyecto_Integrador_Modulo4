# Módulo SQL
Objetivo.- Generar un indice en alguna tabla para mejorar el tiempo de consulta
Solución:
Se tomara como ejemplo la tabla venta y la el campo IdSucursal para crear el índice.
Para crear el índice utilizaremos la base creada en la práctica del README_PARQUET.md
Bd: integrador2
Para esto entramos al contenedor de hive
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/f36c1679-80f3-4807-9c3f-0bf3f35f5ba6)
Ya dentro de hive ejecutamos el siguiente comando:
```
use integrador2;
```

Primero hacemos una consulta antes de generar el indice en la tabla venta

![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/9405fd0d-53eb-4cf3-a0c3-c48cd29e4a13)


Generamos el índice en la tabla con el siguiente comando:

```
CREATE INDEX index_venta_sucursal ON TABLE venta(IdSucursal) AS 'org.apache.hadoop.hive.ql.index.compact.CompactIndexHandler' WITH DEFERRED REBUILD;
```
Hacemos nuevamente la consulta para ver si mejoró el tiempo
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/ca87aae7-b7bf-4f96-b8b9-7fe5bbe633a9)


