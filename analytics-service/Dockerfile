# Base IMG to use eg. runtime, build tool
FROM maven:3.9.9-eclipse-temurin-21 AS builder

# Specify working directory inside container
WORKDIR /app
# Copy dependency
COPY pom.xml .
# Maven install only change dependency
RUN mvn dependency:go-offline -B
# Copy folder
COPY src ./src
# Pack new package to .jar file
RUN mvn clean package
# Run build code
FROM openjdk:21-jdk AS runner

WORKDIR /app

COPY --from=builder ./app/target/analytics-service-0.0.1-SNAPSHOT.jar ./app.jar
# Specify port of app
EXPOSE 4002
# Specify command to run code
ENTRYPOINT ["java", "-jar", "app.jar"]