# syntax=docker/dockerfile:1

FROM maven:3-eclipse-temurin-17-alpine as build
ENV HOME=/usr/app
RUN mkdir -p $HOME
WORKDIR $HOME
# layer 1 - package project (any project changing cause redownloading dependencies)
ADD . $HOME
RUN mvn package

FROM eclipse-temurin:17-jdk-jammy
COPY --from=build /usr/app/target/demo-*.jar /app/demo-app.jar
ENTRYPOINT java -jar /app/demo-app.jar

# build image
# docker build -f Dockerfile_single_layer --tag demo-app .

# run built container (detached)
# docker run --rm -d -p 8080:8080 --name demo-server demo-app

# stop running container
# docker stop demo-server