# Use an official Maven image as a build environment
FROM maven:3.9.9-openjdk:17-jdk-alpine as build
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Run application
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

# Enable DevTools for hot reload
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "-Dspring.devtools.restart.enabled=true", "app.jar"]

# RUN addgroup -S spring && adduser -S spring -G spring
# USER spring:spring
# ARG JAR_FILE=target/*.jar
# COPY ${JAR_FILE} app.jar
# ENTRYPOINT ["java","-jar","/app.jar"]