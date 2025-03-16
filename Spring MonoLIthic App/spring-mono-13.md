# Spring Security Guide

## Table of Contents

- [Introduction to Security](#introduction-to-security)
- [Before Getting Started With Spring Security](#before-getting-started-with-spring-security)
- [How Spring Security Works | Flow and Internal Details](#how-spring-security-works--flow-and-internal-details)
- [Getting Started with Spring Security | Securing Spring Boot Applications](#getting-started-with-spring-security--securing-spring-boot-applications)
- [Understanding the Default Behaviour of Spring Security](#understanding-the-default-behaviour-of-spring-security)
- [More with Form-Based Authentication in Spring Security](#more-with-form-based-authentication-in-spring-security)
- [Writing Your Own Security Filter with Spring Security](#writing-your-own-security-filter-with-spring-security)
- [Form-Based vs Basic Authentication with Spring Security](#form-based-vs-basic-authentication-with-spring-security)
- [Making Basic Authentication Stateless with Spring Security](#making-basic-authentication-stateless-with-spring-security)
- [Working with Postman with Spring Security](#working-with-postman-with-spring-security)
- [In-Memory Authentication with Spring Security](#in-memory-authentication-with-spring-security)
- [Role-Based Authorization with Spring Security](#role-based-authorization-with-spring-security)
- [Enabling H2 Database with Spring Security](#enabling-h2-database-with-spring-security)
- [Using Database to Store User Credentials with Spring Security](#using-database-to-store-user-credentials-with-spring-security)
- [What is Hashing and Why it's Important?](#what-is-hashing-and-why-its-important)
- [Password Encoding and Hashing with Spring Security | Password Security](#password-encoding-and-hashing-with-spring-security--password-security)
- [JWT | What is it and Why Use it with Spring Security? [JSON Web Token]](#jwt--what-is-it-and-why-use-it-with-spring-security-json-web-token)
  - [Understanding the Implementation](#understanding-the-implementation)
  - [Setting up the Project](#setting-up-the-project)
  - [Implementing JwtUtils](#implementing-jwtutils)
  - [Creating Custom Filter for JWT Authentication with Spring Security](#creating-custom-filter-for-jwt-authentication-with-spring-security)
  - [Defining AuthEntryPointJwt](#defining-authentrypointjwt)
  - [Sign-in Flow with JWT and Spring Security](#sign-in-flow-with-jwt-and-spring-security)
- [Managing Security Configurations with Spring Security](#managing-security-configurations-with-spring-security)

---

## Introduction to Security
Security is an essential part of any application to protect user data, prevent unauthorized access, and maintain data integrity. Spring Security is a powerful authentication and access control framework that integrates seamlessly with Spring applications.

## Before Getting Started With Spring Security
Before implementing security features in Spring Boot, it's essential to understand how authentication and authorization work. Spring Security provides a highly customizable security framework that helps protect web applications.

## How Spring Security Works | Flow and Internal Details
Spring Security works through a filter-based architecture. It intercepts HTTP requests, validates authentication credentials, and determines access permissions based on roles and policies.

### Key Components:
- **AuthenticationManager**: Handles authentication logic.
- **SecurityContextHolder**: Stores security context for the current request.
- **UserDetailsService**: Loads user-specific security data.
- **PasswordEncoder**: Ensures password security with hashing algorithms.

## Getting Started with Spring Security | Securing Spring Boot Applications
Spring Boot integrates Spring Security easily with minimal configuration. By default, Spring Boot provides basic authentication.

### Steps:
1. Add Spring Security dependency.
2. Configure security settings.
3. Implement authentication and authorization logic.

## Understanding the Default Behaviour of Spring Security
By default, Spring Security:
- Enables HTTP Basic Authentication.
- Provides a default login page.
- Secures all endpoints unless explicitly configured.

## More with Form-Based Authentication in Spring Security
Form-based authentication allows users to log in using a web form rather than a basic authentication pop-up.

## Writing Your Own Security Filter with Spring Security
You can create custom filters to add additional security layers such as JWT authentication or API key validation.

## Form-Based vs Basic Authentication with Spring Security
| Authentication Type | Features |
|---------------------|----------|
| **Form-Based** | Customizable login page, session-based authentication |
| **Basic** | Browser pop-up login, stateless authentication |

## Making Basic Authentication Stateless with Spring Security
Stateless authentication eliminates session storage by using tokens (like JWT) instead of sessions.

## Working with Postman with Spring Security
Postman can be used to test secured endpoints by providing authentication headers and tokens.

## In-Memory Authentication with Spring Security
Spring Security allows storing user credentials in memory for testing purposes using `UserDetailsService`.

## Role-Based Authorization with Spring Security
Role-based access control (RBAC) restricts resources based on assigned user roles (`ADMIN`, `USER`, etc.).

## Enabling H2 Database with Spring Security
To use H2 with Spring Security, configure the security settings to allow access to the H2 console.

## Using Database to Store User Credentials with Spring Security
Instead of in-memory authentication, credentials can be stored in a relational database using JDBC.

## What is Hashing and Why it's Important?
Hashing ensures that passwords are securely stored by converting plain text into irreversible hashed values.

## Password Encoding and Hashing with Spring Security | Password Security
Spring Security provides `BCryptPasswordEncoder` for secure password hashing.

## JWT | What is it and Why Use it with Spring Security? [JSON Web Token]
JWT is a stateless authentication mechanism where user credentials are encoded into a token.

### Understanding the Implementation
JWT consists of three parts: Header, Payload, and Signature.

### Setting up the Project
Add JWT dependencies and configure security settings.

### Implementing JwtUtils
Create a utility class for generating and validating JWT tokens.

### Creating Custom Filter for JWT Authentication with Spring Security
Implement a custom security filter that validates incoming JWT tokens.

### Defining AuthEntryPointJwt
Handles unauthorized access attempts by returning appropriate HTTP responses.

### Sign-in Flow with JWT and Spring Security
The authentication process includes login, token issuance, and role-based access control.

## Managing Security Configurations with Spring Security
Security configurations define authentication mechanisms, protected routes, and access policies.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
