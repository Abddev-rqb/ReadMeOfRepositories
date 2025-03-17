# Spring Boot Monolithic Application: Database Integration with JPA

## Table of Contents
- [Introduction](#introduction)
- [Different Databases and Magic of JPA](#different-databases-and-magic-of-jpa)
- [MySQL Interface](#mysql-interface)
- [Configuring Application to Work with MySQL](#configuring-application-to-work-with-mysql)
- [Database Schema Management](#database-schema-management)
- [Postgres and PgAdmin](#postgres-and-pgadmin)
- [Configuring Application to Work with PostgreSQL](#configuring-application-to-work-with-postgresql)
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

## Introduction
This guide explores how to integrate different relational databases with a Spring Boot monolithic application using JPA (Java Persistence API). It also covers database schema management and configuration for MySQL and PostgreSQL.

---

## Different Databases and Magic of JPA
JPA simplifies database interactions in a Spring Boot monolithic application. It provides an abstraction layer over different databases, allowing the same entity models and repository interfaces to work with multiple databases like MySQL and PostgreSQL without code changes.

**Key Benefits of JPA:**
- Database independence
- Reduced boilerplate code
- Support for caching and transaction management
- Seamless integration with ORM frameworks like Hibernate

---

## MySQL Interface
MySQL is a widely used relational database management system known for its performance and scalability. Spring Boot supports MySQL via JPA and Hibernate.

**Installing MySQL:**
```sh
sudo apt update
sudo apt install mysql-server
```

**Accessing MySQL CLI:**
```sh
mysql -u root -p
```

---

## Configuring Application to Work with MySQL
### 1. Add MySQL Dependency in `pom.xml`
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 2. Configure `application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
```

---

## Database Schema Management
Spring Boot provides two primary approaches for schema management:

### 1. **Using Hibernate Auto DDL**
Modify `application.properties`:
```properties
spring.jpa.hibernate.ddl-auto=update
```
Options:
- `update` – Updates schema while preserving data
- `create` – Creates schema but removes data
- `create-drop` – Drops and recreates schema

### 2. **Using Flyway or Liquibase** (Recommended for production)
To use Flyway, add:
```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>
```
Create migration scripts in `src/main/resources/db/migration/`.

---

## Postgres and PgAdmin
PostgreSQL is an advanced open-source relational database with strong ACID compliance and performance optimization.

**Installing PostgreSQL:**
```sh
sudo apt update
sudo apt install postgresql postgresql-contrib
```

**Accessing PostgreSQL CLI:**
```sh
sudo -u postgres psql
```

**Installing PgAdmin for GUI-based management:**
```sh
sudo apt install pgadmin4
```

---

## Configuring Application to Work with PostgreSQL
### 1. Add PostgreSQL Dependency
```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 2. Configure `application.properties`
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=postgres
spring.datasource.password=password
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

---

## Conclusion
By leveraging JPA, Spring Boot applications can seamlessly integrate with MySQL and PostgreSQL. Proper schema management using Hibernate, Flyway, or Liquibase ensures data integrity and easy migrations. Understanding these configurations is crucial for building scalable enterprise applications.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)