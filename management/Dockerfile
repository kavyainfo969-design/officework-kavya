# Multi-stage Dockerfile for Spring Boot backend
# Stage 1: build with Maven
FROM maven:3.8.7-eclipse-temurin-17 AS build
WORKDIR /workspace

# Copy pom and source, build the app
COPY pom.xml ./
COPY src ./src
RUN mvn -B -DskipTests package

# Stage 2: runtime image
FROM eclipse-temurin:17-jre-alpine
ARG JAR_FILE=target/management-0.0.1-SNAPSHOT.jar
COPY --from=build /workspace/${JAR_FILE} /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
