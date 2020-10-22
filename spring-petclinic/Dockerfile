FROM maven:3.6.3-jdk-8 AS maven
WORKDIR /app
COPY pom.xml pom.xml
COPY src src
RUN mvn package
RUN mv target/*.jar target/app.jar
CMD ["java", "-jar", "target/app.jar"]
