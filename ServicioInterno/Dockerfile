FROM maven:3.6.0-jdk-8-alpine as builder
COPY ./pom.xml /project/pom.xml
COPY ./src /project/src
WORKDIR /project
RUN mvn dependency:go-offline
RUN mvn -DskipTests=true package

FROM openjdk:8-jre
RUN apt-get update && apt-get install -y netcat
RUN mkdir /internalService
COPY --from=builder /project/target/*.jar /internalService
WORKDIR /internalService
EXPOSE 8070
CMD java -jar ServicioInterno-0.0.1-SNAPSHOT.jar