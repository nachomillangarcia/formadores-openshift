# Tomcat Sample

## Construir y desplegar
```
docker build -t tomcat-sample .
docker run -p 8080:80 tomcat-sample
```

## Desplegar la imagen subida a DockerHub
```
docker run -p 8080:8080 nachomillangarcia/tomcat
```

Accede a [http://localhost:8080/](http://localhost:8080/)