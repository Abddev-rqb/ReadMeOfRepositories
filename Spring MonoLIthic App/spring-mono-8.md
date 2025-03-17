# Lombok: Simplify Java Development

## Table of Contents
- [What is Lombok?](#what-is-lombok)
- [Lombok Annotations You Should Know](#lombok-annotations-you-should-know)
  - [@Getter and @Setter](#getter-and-setter)
  - [@ToString](#tostring)
  - [@EqualsAndHashCode](#equalsandhashcode)
  - [@NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor](#noargsconstructor-allargsconstructor-requiredargsconstructor)
  - [@Data](#data)
  - [@Builder](#builder)
  - [@Slf4j](#slf4j)
- [Lombok Plugin and Annotation Processing](#lombok-plugin-and-annotation-processing)
- [Lombok in Action](#lombok-in-action)
- [Conclusion](#conclusion)

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

## What is Lombok?
Lombok is a Java library that helps reduce boilerplate code by automatically generating commonly used methods like getters, setters, constructors, and toString methods at compile time. It improves developer productivity and keeps code clean.

### Features of Lombok:
- Reduces boilerplate code
- Improves readability and maintainability
- Supports Java and various frameworks

To use Lombok, add the following dependency to your `pom.xml` (Maven):

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.28</version>
    <scope>provided</scope>
</dependency>
```

For Gradle:

```gradle
dependencies {
    compileOnly 'org.projectlombok:lombok:1.18.28'
    annotationProcessor 'org.projectlombok:lombok:1.18.28'
}
```

---

## Lombok Annotations You Should Know

### @Getter and @Setter
Generates getter and setter methods for fields automatically.

```java
import lombok.Getter;
import lombok.Setter;

public class User {
    @Getter @Setter
    private String name;
    @Getter @Setter
    private int age;
}
```

### @ToString
Generates a `toString()` method for the class.

```java
import lombok.ToString;

@ToString
public class User {
    private String name;
    private int age;
}
```

### @EqualsAndHashCode
Generates `equals()` and `hashCode()` methods.

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class User {
    private String name;
    private int age;
}
```

### @NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor
Generates constructors automatically.

```java
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;
import lombok.RequiredArgsConstructor;

@NoArgsConstructor
@AllArgsConstructor
@RequiredArgsConstructor
public class User {
    private String name;
    private int age;
}
```

### @Data
A shortcut for `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, and `@RequiredArgsConstructor`.

```java
import lombok.Data;

@Data
public class User {
    private String name;
    private int age;
}
```

### @Builder
Provides a builder pattern for object creation.

```java
import lombok.Builder;

@Builder
public class User {
    private String name;
    private int age;
}
```

### @Slf4j
Generates a logger instance.

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class LoggerExample {
    public static void main(String[] args) {
        log.info("Lombok logging in action!");
    }
}
```

---

## Lombok Plugin and Annotation Processing

### Installing Lombok Plugin
1. Install the Lombok plugin for your IDE (IntelliJ IDEA, Eclipse, VS Code).
2. Enable annotation processing in your IDE settings.

### Enable Annotation Processing
For IntelliJ IDEA:
- Go to **Settings > Build, Execution, Deployment > Compiler > Annotation Processors**
- Check **Enable annotation processing**

For Eclipse:
- Go to **Preferences > Java > Compiler > Annotation Processing**
- Enable annotation processing

---

## Lombok in Action
Here’s a complete example demonstrating Lombok’s power:

```java
import lombok.*;
import lombok.extern.slf4j.Slf4j;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
@Slf4j
public class Employee {
    private String name;
    private int id;
    private double salary;

    public static void main(String[] args) {
        Employee emp = Employee.builder().name("John Doe").id(101).salary(50000.0).build();
        log.info("Employee Details: {}", emp);
    }
}
```

---

## Conclusion
Lombok significantly reduces Java boilerplate code, improves readability, and enhances developer productivity. By using annotations like `@Getter`, `@Setter`, `@Data`, and `@Builder`, Java developers can write clean, concise, and maintainable code.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)