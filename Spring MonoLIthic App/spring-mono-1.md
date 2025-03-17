# Web and API Fundamentals

## Table of Contents
- [How Does the Web Work?](#how-does-the-web-work)
- [What is a Client-Server?](#what-is-a-client-server)
- [What are APIs?](#what-are-apis)
- [Types of API Requests](#types-of-api-requests)
- [What is REST API and its Architecture?](#what-is-rest-api-and-its-architecture)
- [HTTP vs HTTPS](#http-vs-https)
- [What are Status Codes?](#what-are-status-codes)
- [What is Resource, URI, and Sub-Resource?](#what-is-resource-uri-and-sub-resource)

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

## How Does the Web Work?
The web operates using a **Client-Server** architecture. When a user requests a web page:
1. The **browser (client)** sends a request to the **server** (where the website is hosted).
2. The **server** processes the request and sends back the required response.
3. The **browser** renders the response for the user to interact with.

This interaction happens over the **HTTP/HTTPS** protocol using requests like `GET`, `POST`, etc.

---

## What is a Client-Server?
A **Client-Server** model consists of:
- **Client**: A device or software (e.g., web browser) that sends requests to the server.
- **Server**: A system that responds to client requests by serving data, processing logic, or other services.

Example:
```
Client (Browser) → HTTP Request → Server (Backend) → HTTP Response → Client
```

---

## What are APIs?
API (Application Programming Interface) is a set of rules that allows software components to communicate. APIs define methods and data formats applications can use to interact with other software components.

For example, when you use a payment gateway like PayPal, an API is used to process the transaction.

---

## Types of API Requests
APIs support various HTTP methods:

| HTTP Method | Description |
|------------|-------------|
| GET | Retrieve data from the server |
| POST | Send data to the server |
| PUT | Update existing data |
| DELETE | Remove data from the server |
| PATCH | Partially update data |

Example:
```bash
GET https://api.example.com/users
POST https://api.example.com/users
```

---

## What is REST API and its Architecture?
A **RESTful API** follows REST principles:
- **Stateless**: Each request contains all necessary information.
- **Client-Server Architecture**: The client and server operate independently.
- **Resource-based**: Uses URIs to represent resources.
- **Use of HTTP methods**: Standardized communication.

Example:
```json
{
  "user": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

---

## HTTP vs HTTPS
| Feature  | HTTP  | HTTPS  |
|----------|------|------|
| Security | Unencrypted | Encrypted with SSL/TLS |
| Port | 80 | 443 |
| Data Integrity | Vulnerable | Secure |
| Usage | General websites | Banking, e-commerce |

Always prefer **HTTPS** for secure communication.

---

## What are Status Codes?
HTTP response status codes indicate the outcome of an API request:

| Code | Meaning |
|------|---------|
| 200 | OK (Successful Request) |
| 201 | Created (Resource Created Successfully) |
| 400 | Bad Request (Invalid Input) |
| 401 | Unauthorized (Authentication Required) |
| 403 | Forbidden (Access Denied) |
| 404 | Not Found (Resource Unavailable) |
| 500 | Internal Server Error |

Example:
```bash
HTTP/1.1 200 OK
```

---

## What is Resource, URI, and Sub-Resource?
- **Resource**: A data entity (e.g., user, order, product).
- **URI (Uniform Resource Identifier)**: The address to access a resource.
- **Sub-Resource**: A nested resource within another resource.

Example URIs:
```
/users → Main Resource
/users/1 → Specific User
/users/1/orders → Sub-Resource (Orders of User 1)
```

---

## 📌 Best Practices
- Always use **HTTPS** for secure communication.
- Implement **proper status codes** for API responses.
- Structure URIs in a **RESTful manner**.
- Use **pagination** for large datasets.
- Implement **API versioning** (e.g., `/v1/users`).

📢 Star ⭐ this repository if you found it helpful!

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
