# Stage 1: Build
FROM maven:3.8.4-openjdk-8-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run
FROM openjdk:8-jre-alpine
MAINTAINER Saanvi Rajput <saanvi@example.com>

# Add Non-root user for security
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

COPY --from=build /app/target/account-service.jar /app/account-service.jar
ENTRYPOINT ["java", "-Xmx200m", "-jar", "/app/account-service.jar"]

EXPOSE 6000