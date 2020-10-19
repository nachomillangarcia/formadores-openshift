# web-docker-sesion-1

## Construir y desplegar
```
mvn package
docker build -t formadoresit-nginx .
docker run -p 8080:80 formadoresit-nginx
```

## Desplegar la imagen subida a DockerHub
```
docker run -p 8080:8080 nachomillangarcia/formadoresit-nginx
```

Accede a [http://localhost:8080/](http://localhost:8080/)