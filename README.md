Prerequisites
JDK 17 or later
Maven or Gradle
Docker installed on your machine
IDE (IntelliJ IDEA, Eclipse, etc.)
Step 1: Set Up a Spring Boot Project
Use Spring Initializr to create a new project with the following configuration:

Project: Maven Project
Language: Java
Spring Boot: 3.2.x
Dependencies: Spring Web
Download and unzip the project, then open it in your IDE.

Example Spring Boot Application
Create a simple Spring Boot application with a REST controller.

1.1 Application Class
package com.example.dockerproject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class dockerprojectApplication {

    public static void main(String[] args) {
        SpringApplication.run(dockerprojectApplication.class, args);
    }
}
1.2 REST Controller
Create a REST controller class named HelloController in the com.example.dockerproject.controller package.

package com.example.dockerproject.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Docker!";
    }
}
1.3 Maven Configuration
Ensure that your pom.xml is configured correctly. The default configuration provided by Spring Initializr should suffice.

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!-- Additional dependencies can be added here -->
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
Step 2: Create a Dockerfile
A Dockerfile is a script containing instructions to build a Docker image.

2.1 Create a Dockerfile
Create a file named Dockerfile in the root directory of your project.

# Use the official OpenJDK base image
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built jar file into the container
COPY target/dockerproject.jar app.jar

# Expose port 8080
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
Explanation:

FROM openjdk:17-jdk-alpine: Uses the official OpenJDK base image with JDK 17.
WORKDIR /app: Sets the working directory inside the container to /app.
COPY target/dockerproject.jar app.jar: Copies the built jar file from the target directory into the container.
EXPOSE 8080: Exposes port 8080 to the host.
ENTRYPOINT ["java", "-jar", "app.jar"]: Specifies the command to run the application.
Step 3: Build the Spring Boot Application
3.1 Build the Jar File
Run the following command to build the jar file of your Spring Boot application:

./mvnw clean package
This command will generate a jar file in the target directory, for example, target/dockerproject-0.0.1-SNAPSHOT.jar.

Step 4: Build the Docker Image
4.1 Build the Docker Image
Run the following command to build the Docker image:

docker build -t dockerproject-app .
Explanation:

docker build: The Docker command to build an image.
-t dockerproject-app: Tags the image with the name dockerproject-app.
.: Specifies the current directory as the build context.
Step 5: Run the Docker Container
5.1 Run the Docker Container
Run the following command to start a Docker container from the image:

docker run -p 8080:8080 dockerproject-app
Explanation:

docker run: The Docker command to run a container.
-p 8080:8080: Maps port 8080 of the container to port 8080 on the host machine.
dockerproject-app: The name of the Docker image to run.
Step 6: Test the Application
6.1 Access the Application
Open a web browser or a tool like Postman and navigate to the following URL:

http://localhost:8080/hello
You should see the message "Hello, Docker!" returned from the HelloController.

Step 7: Additional Docker Commands
7.1 List Docker Images
To list all Docker images on your system, run:

docker images
7.2 List Running Containers
To list all running Docker containers, run:

docker ps
7.3 Stop a Running Container
To stop a running Docker container, run:

docker stop <container_id>
Replace <container_id> with the actual container ID obtained from the docker ps command.

7.4 Remove a Docker Container
To remove a Docker container, run:

docker rm <container_id>
Replace <container_id> with the actual container ID.

7.5 Remove a Docker Image
To remove a Docker image, run:

docker rmi dockerproject-app
