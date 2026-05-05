# Use official Maven image to build the app
FROM maven:3.9.9-eclipse-temurin-17 AS build

# Set working directory
WORKDIR /app

# Copy project files
COPY . .

# Build the application
RUN mvn clean package -DskipTests

# Use lightweight JDK image to run
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copy the built jar from previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose port (Render uses 10000 internally but we bind dynamically)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java","-jar","app.jar"]
