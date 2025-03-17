
# Database Basics: Understanding Data and Databases

## Table of Contents

- [Introduction](#introduction)
- [What is DBMS?](#what-is-dbms)
- [Introduction to Relational Database Concepts](#introduction-to-relational-database-concepts)
- [Overview of SQL](#overview-of-sql)
- [What is ORM?](#what-is-orm)
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

In today's digital world, data is the backbone of businesses. Managing this data efficiently requires a well-structured database management system. This guide introduces the basics of databases, relational databases, SQL, and ORM (Object-Relational Mapping).

---

## What is DBMS?

A **Database Management System (DBMS)** is software that allows users to store, retrieve, and manage data efficiently. It provides an interface for interacting with databases while ensuring data integrity, security, and consistency.

### Key Features of DBMS:
- Data Storage and Retrieval
- Data Security and Access Control
- Data Integrity and Consistency
- Backup and Recovery
- Multi-User Access and Concurrency Control

Popular DBMS examples include **MySQL, PostgreSQL, MongoDB, and Oracle DB**.

---

## Introduction to Relational Database Concepts

A **Relational Database Management System (RDBMS)** is a type of DBMS that stores data in structured tables with rows and columns. The relationships between these tables are maintained using **keys**.

### Key Concepts:
- **Table:** A structured format for storing data in rows and columns.
- **Primary Key:** A unique identifier for each record in a table.
- **Foreign Key:** A field in a table that references the primary key of another table.
- **Normalization:** A technique to reduce data redundancy and improve database efficiency.
- **ACID Properties:** Ensures **Atomicity, Consistency, Isolation, and Durability** in transactions.

**Example Table Structure:**
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

---

## Overview of SQL

**SQL (Structured Query Language)** is used to interact with relational databases. It allows users to create, read, update, and delete (CRUD) data.

### Common SQL Commands:
- **Data Query:** `SELECT` statement to retrieve data
- **Data Modification:** `INSERT`, `UPDATE`, `DELETE`
- **Data Definition:** `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`
- **Data Control:** `GRANT`, `REVOKE` for user access control

**Example SQL Queries:**
```sql
-- Creating a table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100)
);

-- Inserting data
INSERT INTO Customers (CustomerID, Name, Email) VALUES (1, 'John Doe', 'john@example.com');

-- Retrieving data
SELECT * FROM Customers;

-- Updating data
UPDATE Customers SET Email = 'john.doe@example.com' WHERE CustomerID = 1;

-- Deleting data
DELETE FROM Customers WHERE CustomerID = 1;
```

---

## What is ORM?

**Object-Relational Mapping (ORM)** is a technique used in programming to interact with a database using object-oriented paradigms instead of writing SQL queries manually.

ORM frameworks allow developers to map database tables to objects in their preferred programming language, reducing the need for raw SQL queries.

### Benefits of ORM:
- Simplifies database interactions
- Reduces boilerplate SQL code
- Improves database portability across different systems
- Enhances security by preventing SQL injection attacks

### Popular ORM Frameworks:
- **Hibernate (Java)**
- **SQLAlchemy (Python)**
- **Entity Framework (C#)**
- **Sequelize (Node.js)**

**Example using SQLAlchemy (Python ORM):**
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)

# Database connection
engine = create_engine('sqlite:///users.db')
Base.metadata.create_all(engine)
Session = sessionmaker(bind=engine)
session = Session()

# Adding a new user
new_user = User(name='Alice', email='alice@example.com')
session.add(new_user)
session.commit()
```

---

## Conclusion

Understanding databases and their management is crucial for building scalable and efficient applications. SQL enables seamless data manipulation, while ORM simplifies database interactions, making development more productive.

If you're looking to enhance your database skills further, explore advanced topics like indexing, database optimization, and distributed databases.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)

