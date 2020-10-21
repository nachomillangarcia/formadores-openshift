
Para construir y ejecutar la app

```
docker build -t java-todo .
docker run -d -e MYSQL_ROOT_PASSWORD=pass -e MYSQL_DATABASE=todo -e MYSQL_USER=todo -e MYSQL_PASSWORD=pass --name mysql mysql
docker run -d --link mysql -e DB_HOSTNAME=mysql -e DB_NAME=todo -e DB_USERNAME=todo -e DB_PASSWORD=pass -p 8080:8080 java-todo
```

Para simplemente ejecutar la imagen disponible en mi DockerHub:

```
docker run -d -e MYSQL_ROOT_PASSWORD=pass -e MYSQL_DATABASE=todo -e MYSQL_USER=todo -e MYSQL_PASSWORD=pass --name mysql mysql
docker run -d --link mysql -e DB_HOSTNAME=mysql -e DB_NAME=todo -e DB_USERNAME=todo -e DB_PASSWORD=pass -p 8080:8080 nachomillangarcia/java-todo
```

Acceder a [http://localhost:8080/login](http://localhost:8080/login)

Usuario: formadoresit

Contraseña: dummy

## Docker Compose

Construir las imágenes

`docker-compose build`

Levantar todos los servicios

`docker-compose up`

