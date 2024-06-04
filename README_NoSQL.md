# Módulo NoSQL
Levantar el contenedor de HBase empleando el 
```
sudo docker-compose -f docker-compose-v3.yml up -d
```
![image](https://github.com/OscarMoralesMejia/Proyecto_Integrador_Modulo4/assets/159685580/f012031f-5f1b-42e1-9fdf-2235cb61c65d)

Podemos entrar al contenedor con el siguiente comando
```
sudo docker exec -it hbase-master hbase shell
```
Tuve un problema al dejarlo correr y hacer otras cosas , automaticamente se bajo el servicio de hbase-master
docker run -d --name hbase-master --network hbase-network harisekhon/hbase

