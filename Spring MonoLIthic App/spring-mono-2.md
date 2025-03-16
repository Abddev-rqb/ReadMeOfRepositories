# Java Spring Framework Concepts

## Table of Contents

1. [What is a Web Framework?](#what-is-a-web-framework)
2. [Introduction to Spring Framework](#introduction-to-spring-framework)
3. [Tight Coupling vs. Loose Coupling](#tight-coupling-vs-loose-coupling)
4. [Hands-On: Tight Coupling and Loose Coupling](#hands-on-tight-coupling-and-loose-coupling)
5. [Core Concepts of Spring Framework](#core-concepts-of-spring-framework)
6. [Spring Container and Configuration](#spring-container-and-configuration)
7. [Setting Up a Spring Project](#setting-up-a-spring-project)
8. [Creating Your First Bean](#creating-your-first-bean)
9. [Lifecycle of a Bean](#lifecycle-of-a-bean)
10. [Dependency Injection (DI)](#dependency-injection-di)
11. [Constructor Injection](#constructor-injection)
12. [Setter Injection](#setter-injection)
13. [Challenge: Inversion of Control (IoC)](#challenge-inversion-of-control-ioc)
14. [Introduction to Autowiring](#introduction-to-autowiring)
15. [Autowiring by Name](#autowiring-by-name)
16. [Autowiring by Type](#autowiring-by-type)
17. [Autowiring by Constructor](#autowiring-by-constructor)

---

## What is a Web Framework?

A web framework is a software platform that simplifies the development of web applications by providing reusable components, libraries, and a structured way to build applications.

---

## Introduction to Spring Framework

Spring is a powerful, lightweight, and flexible framework for Java applications. It provides support for developing Java EE applications with minimal configuration.

**Key Features:**
- Inversion of Control (IoC)
- Aspect-Oriented Programming (AOP)
- Dependency Injection (DI)
- Transaction Management
- Integration with various frameworks

---

## Tight Coupling vs. Loose Coupling

**Tight Coupling:** When classes are highly dependent on each other.

**Loose Coupling:** When classes have minimal dependency, making code more modular and testable.

Example:
```java
class A {
    B objB = new B();
}
```
Here, class `A` depends on `B`, leading to **tight coupling**.

In **loose coupling**, dependency is injected at runtime:
```java
class A {
    B objB;
    A(B objB) { this.objB = objB; }
}
```

---

## Hands-On: Tight Coupling and Loose Coupling

Create two classes demonstrating tight and loose coupling and test them with a `main` method.

---

## Core Concepts of Spring Framework

- **Spring Container**
- **Beans**
- **IoC (Inversion of Control)**
- **Dependency Injection**
- **Spring MVC**
- **AOP (Aspect-Oriented Programming)**

---

## Spring Container and Configuration

Spring Container is responsible for managing the lifecycle of beans. It is configured using:
- XML Configuration
- Java-based Configuration
- Annotation-based Configuration

---

## Setting Up a Spring Project

1. Install **Spring Boot** via Spring Initializr
2. Add dependencies in `pom.xml` (Maven) or `build.gradle` (Gradle)
3. Configure `application.properties`
4. Create a **Spring Configuration Class**

---

## Creating Your First Bean

```java
@Component
public class HelloWorld {
    public void sayHello() {
        System.out.println("Hello, Spring!");
    }
}
```

---

## Lifecycle of a Bean

1. **Instantiation**
2. **Initialization**
3. **Destruction**

Example:
```java
@Bean(initMethod = "init", destroyMethod = "cleanup")
public MyBean myBean() {
    return new MyBean();
}
```

---

## Dependency Injection (DI)

Spring supports DI using:
- Constructor Injection
- Setter Injection
- Field Injection

---

## Constructor Injection

```java
@Component
class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

@Component
class Car {
    private Engine engine;
    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

---

## Setter Injection

```java
@Component
class Car {
    private Engine engine;
    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```

---

## Challenge: Inversion of Control (IoC)

Try to implement IoC using XML or Java-based configuration.

---

## Introduction to Autowiring

Autowiring enables automatic dependency injection by Spring.

Types:
1. **By Name**
2. **By Type**
3. **By Constructor**

---

## Autowiring by Name

```java
@Autowired
@Qualifier("engine")
private Engine engine;
```

---

## Autowiring by Type

```java
@Autowired
private Engine engine;
```

---

## Autowiring by Constructor

```java
@Autowired
public Car(Engine engine) {
    this.engine = engine;
}
```

---

## Conclusion

This guide provides an overview of the Spring Framework, covering core concepts like dependency injection, bean lifecycle, and autowiring. Follow this repository for more Spring-based projects.

---

## Contributing

Feel free to fork this repo and contribute!

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
