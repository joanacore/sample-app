# Stage 1: Build the Spring Boot application
FROM maven:3.9.4-eclipse-temurin-17 AS builder

# Install Git to clone the repository
RUN apt-get update && apt-get install -y git && apt-get clean

# Set the working directory
RUN mkdir -p /app/
WORKDIR /app

# Clone the Git repository (replace with your repository URL)
RUN git clone https://github.com/joanacore/sample-app.git

RUN chmod -R 777 /app/sample-app

WORKDIR /app/sample-app

# Build the Maven project and package the application
RUN mvn clean package -DskipTests

# Stage 2: Run the Spring Boot application
FROM eclipse-temurin:17-jre-alpine

# Set working directory for the runtime container
WORKDIR /app

# Copy the JAR file from the builder stage
COPY --from=builder /app/sample-app/target/*.jar app.jar

# Expose the port that Spring Boot runs on (default: 8080)
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]