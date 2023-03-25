# Crear un servidor de MYSQL mediante Docker

### 1. Descargar la imagen de MYSQL from Docker Hub 

```
docker pull mysql:8

```
### 2. Verificar la imagen de MYSQL desde la lista de imágenes de Docker
```
docker images
docker images | grep mysql (linux/mac)
docker images | findStr mysql (filtrar listas con windows)
```

### 3. Crear un contenedor con la imagen de MYSQL
```
docker create mysql:8 (con nombre aleatorio)
docker create --name mysqlserver mysql:8 (con nombre personalizado)
```

### 4. Para listar los contenedores
```
docker ps -a (te lista todos los contenedores independientes de su status)
docker ps -a | findStr davinci (para filtrar contenedores independientes de su status)
docker ps (solo lo que estén ejecutándose)
docker ps | findStr davinci (para filtrar contenedores que estén ejecutándose)
```

### 5. Para iniciar el contenedor
```
docker start mysqlserver | id

```

### 6. Para ver los procesos dentro de un contenedor
```
docker logs mysqlserver

```

### Para eliminar un contenedor
```
docker rm -f mysqlserver | id

```

### 7. Para crear variables de entorno (obligatorio) y exponer el puerto fuera de la red de docker
```
docker run -d --name mysqlserver -p 3310:3306 -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=cursonode mysql:8

```

### Para detener un contenedor
```
docker stop mysqlserver (duerme el proceso pero sigue activo)
docker kill mysqlserver (mata el proceso padre y sus subprocesos)

```

### Para buscar el directorio de persistencia de una imagen
```
docker inspect mysql:8 (buscar la propiedad volumes)
ir a la doc. del docker hub de esa imagen y buscar el titulo where to store data

```

### 8. Para vincular un volumen al contenedor - persistencia con vol. anónimo
```
docker run -d --name mysqlserver -p 3310:3306 -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=cursonode mysql:8

```

### Para eliminar un contenedor con su volumen anónimo
```
docker rm -fv mysqlserver | id

```

### Para listar volúmenes
```
docker volume ls
docker volume ls | grep vol-nginx (linux/mac)
docker volume ls | findStr vol-nginx (windows)

```

### Para eliminar volúmenes anónimos o nombrados
```
docker volume rm vol-mysql

```

### 9. Para vincular un volumen al contenedor - persistencia con vol. host
```
docker run -d --name mysqlserver -p 3310:3306 -v E:\\docker_examples\\docker\\volume\\mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=cursonode mysql:8

```

### Para eliminar volúmen host
```
Solo debes eliminar el directorio local creado

```

### 10. Para vincular un volumen al contenedor - persistencia con vol. nombrado (recomendado)
```
docker run -d --name mysqlserver -p 3310:3306 -v vol-mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=cursonode mysql:8

```

### Crear una red
```´
3 tipos: bridge (default/named bridge), host, none
docker network create net-mysql -d bridge

```

### 3. Listas redes
```´
docker network ls
docker network ls | grep net-mysql (linux/mac)
docker network ls | findStr net-mysql (windows)

```

### Inspeccionar redes
```´
docker network inspect net-mysql

```

### Conectarme a una red
```´
docker run -d --name mysqlserver --network net-mysql -p 3310:3306 -v vol-mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=cursonode mysql:8

docker network connect net-mysql mysqlserver

```

### Desvincularse de una red
```´
docker network disconnect net-mysql mysqlserver
```



