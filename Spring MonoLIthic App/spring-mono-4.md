# Spring Boot Introduction

## Table of Contents
1. [Introduction to Spring Boot](#introduction-to-spring-boot)
2. [How Does Spring Boot Work? - Architecture](#how-does-spring-boot-work---architecture)
3. [Getting Started with Spring Initializer](#getting-started-with-spring-initializer)
4. [Setting up and Understanding a Spring Boot Project in IntelliJ](#setting-up-and-understanding-a-spring-boot-project-in-intellij)
5. [Dependencies in Spring Boot](#dependencies-in-spring-boot)
6. [Designing our First Hello World API](#designing-our-first-hello-world-api)
7. [How Did Our API Work?](#how-did-our-api-work)
8. [Understanding Spring Boot Auto-Configuration](#understanding-spring-boot-auto-configuration)
9. [Introduction to application.properties](#introduction-to-applicationproperties)
10. [Creating a POST Request](#creating-a-post-request)
11. [Introduction and Setup for POSTMAN](#introduction-and-setup-for-postman)
12. [Completing Setup of POSTMAN](#completing-setup-of-postman)
13. [Getting JSON Response](#getting-json-response)
14. [Using @PathVariable](#using-pathvariable)

---

## Technology Stack
- Java 17
- Spring Boot 3.x
- Spring Data JPA (Hibernate)
- Spring Security (JWT Authentication)
- MySQL Database
- Lombok
- Postman (for testing)
- Maven

---

## Introduction to Spring Boot
Spring Boot is an extension of the Spring framework that simplifies the setup, configuration, and deployment of Spring applications. It provides embedded servers, auto-configuration, and production-ready features to speed up development.

## How Does Spring Boot Work? - Architecture
Spring Boot follows a layered architecture:
1. **Presentation Layer** - Handles incoming requests (Controllers, REST APIs).
2. **Business Layer** - Implements business logic (Services, Components).
3. **Persistence Layer** - Manages database interactions (Repositories, JPA Entities).
4. **Database Layer** - Stores application data.

## Getting Started with Spring Initializer
Spring Initializer (https://start.spring.io/) is a tool for generating a Spring Boot project with pre-configured dependencies.

Steps:
1. Go to [Spring Initializer](https://start.spring.io/)
2. Select project type: **Maven**
3. Choose **Spring Boot Version**
4. Add dependencies: **Spring Web, Spring Boot DevTools**
5. Generate & download the project
6. Extract and open it in **IntelliJ IDEA**

## Setting up and Understanding a Spring Boot Project in IntelliJ
1. Import the downloaded project.
2. Ensure JDK 17+ is installed.
3. Open `src/main/java/com/example/demo/DemoApplication.java`.
4. Run the `main` method to start the Spring Boot application.

## Dependencies in Spring Boot
Dependencies are defined in `pom.xml` (for Maven projects). Example:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
This dependency enables REST API development in Spring Boot.

## Designing our First Hello World API
Create a controller:
```java
@RestController
@RequestMapping("/api")
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```
Run the application and visit `http://localhost:8080/api/hello`.

## How Did Our API Work?
- `@RestController` - Defines a RESTful API controller.
- `@RequestMapping("/api")` - Base URL mapping.
- `@GetMapping("/hello")` - Handles GET requests.

## Understanding Spring Boot Auto-Configuration
Spring Boot auto-configures beans based on the dependencies present in `pom.xml`, reducing the need for manual configurations.

## Introduction to application.properties
The `application.properties` file is used for configuration:
```properties
server.port=8081
spring.application.name=DemoApp
```
This changes the server port and app name.

## Creating a POST Request
```java
@RestController
@RequestMapping("/api")
public class UserController {
    @PostMapping("/user")
    public String createUser(@RequestBody User user) {
        return "User " + user.getName() + " created!";
    }
}
```
Model class:
```java
public class User {
    private String name;
    // Getters and Setters
}
```

## Introduction and Setup for POSTMAN
Postman is a tool to test APIs:
1. Install Postman.
2. Set up a `POST` request to `http://localhost:8080/api/user`.
3. Send JSON data in the request body.

## Completing Setup of POSTMAN
1. Choose `POST` method.
2. Set `Content-Type: application/json`.
3. Provide request body:
```json
{
    "name": "John Doe"
}
```
4. Click `Send` and check the response.

## Getting JSON Response
Modify the `UserController`:
```java
@PostMapping("/user")
public ResponseEntity<User> createUser(@RequestBody User user) {
    return ResponseEntity.ok(user);
}
```
Response:
```json
{
    "name": "John Doe"
}
```

## Using @PathVariable
`@PathVariable` extracts values from the URL.
```java
@GetMapping("/user/{id}")
public String getUser(@PathVariable int id) {
    return "User ID: " + id;
}
```
Calling `http://localhost:8080/api/user/5` returns:
```
User ID: 5
```

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
