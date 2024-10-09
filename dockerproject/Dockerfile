# Use the official OpenJDK base image
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built jar file into the container
COPY target/*.jar app.jar

# Expose port 8080
EXPOSE 8686

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]