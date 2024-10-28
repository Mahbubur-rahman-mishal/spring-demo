# Use an official Maven image as a build environment
FROM maven:3.9.9 AS build
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:resolve
COPY src ./src
RUN mvn clean package -DskipTests

# Run application
FROM openjdk:21-jdk-slim

# Install Java (OpenJDK) and any required tools
# RUN apt-get update && \
#     apt-get install -y openjdk-17-jre && \
#     apt-get clean

WORKDIR /app
COPY --from=build /build/target/*.jar app.jar

RUN echo $(ls -la)

EXPOSE 8080

# Run the application
# ENTRYPOINT ["java", "-Dspring.devtools.restart.enabled=true", "-jar", "/app/app.jar"]
ENTRYPOINT ["java", \
            "-Dspring.devtools.restart.enabled=true", \
            "-Dspring.devtools.livereload.enabled=true", \
            "-Dspring.devtools.remote.secret=mysecret", \
            "-jar", "/app/app.jar"]