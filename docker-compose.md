# Docker Compose Commands

### Para ejecutar un docker-compose.yaml

```
docker compose up -d

```

### Para eliminar

```
docker compose down

```

### Para ver el estado de los contenedores generados por docker compose

```
docker compose ps
docker compose ps | grep mysql-server (linux/mac)
docker images | findStr mysql-server (filtrar listas con windows)

```

### Para ejecutar solamente algunos servicios

```
docker compose up -d
docker compose up -d <nombre del servicio1> <nombre del servicio2> ...
```