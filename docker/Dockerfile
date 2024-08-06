# use the image for spring boot application build process
FROM maven:3.6.3-openjdk-11-slim AS build

# set the working directory
WORKDIR /app

# copy required files
RUN mkdir helloworld-web-microprofile-openliberty
COPY ./pom.xml .
COPY ./helloworld-web-microprofile-openliberty/src ./helloworld-web-microprofile-openliberty
COPY ./helloworld-web-microprofile-openliberty/pom.xml ./helloworld-web-microprofile-openliberty

# Run the build command to build app
RUN cd helloworld-web-microprofile-openliberty && mvn package

# stage 2 smaller iimage for previous stage
FROM openjdk:11-jre-slim

WORKDIR /app

COPY --from=build /app/helloworld-web-microprofile-openliberty/target/hello-world.jar .

EXPOSE 8080

CMD ["java","-jar","/app/hello-world.jar"]