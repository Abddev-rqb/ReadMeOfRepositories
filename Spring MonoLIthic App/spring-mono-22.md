# Spring Boot Monolithic Application

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Project Setup](#project-setup)
- [Routing Setup](#routing-setup)
- [Navbar Configuration](#navbar-configuration)
- [Home Page](#home-page)
  - [Setting up Banner](#setting-up-banner-on-home-page)
  - [Displaying Products](#displaying-products-on-home-page)
- [Building Pages](#building-pages)
  - [About Page](#building-the-about-page)
  - [Contact Page](#building-the-contact-page)
- [Running the Application](#running-the-application)
- [Contributing](#contributing)
- [License](#license)

## Introduction
This is a monolithic Spring Boot application demonstrating fundamental web development features such as routing, navigation, and dynamic content rendering. The project is structured to be easily scalable and follows best practices for modern Spring Boot applications.

## Features
- Centralized Routing Mechanism
- Dynamic Home Page with Banner & Product Display
- Structured Navigation Bar
- About and Contact Pages
- Responsive UI Design

## Technologies Used
- **Spring Boot** - Backend framework
- **Thymeleaf** - Template rendering
- **Spring MVC** - Routing & Controller logic
- **Spring Data JPA** - Database integration
- **H2/MySQL** - Database options
- **Bootstrap & CSS** - UI styling

## Project Setup
1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/spring-boot-monolithic.git
   cd spring-boot-monolithic
   ```
2. Install dependencies:
   ```sh
   mvn clean install
   ```
3. Run the application:
   ```sh
   mvn spring-boot:run
   ```

## Routing Setup
Spring Boot routes are defined using `@Controller` classes. Example:
```java
@Controller
public class HomeController {
    @GetMapping("/")
    public String home(Model model) {
        model.addAttribute("message", "Welcome to Our Store");
        return "home";
    }
}
```

## Navbar Configuration
Located in `src/main/resources/templates/fragments/navbar.html`:
```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="/">Brand</a>
    <div class="collapse navbar-collapse">
        <ul class="navbar-nav">
            <li class="nav-item"><a class="nav-link" href="/about">About</a></li>
            <li class="nav-item"><a class="nav-link" href="/contact">Contact</a></li>
        </ul>
    </div>
</nav>
```

## Home Page
### Setting up Banner on Home Page
Banner setup in `home.html`:
```html
<div class="jumbotron">
    <h1 th:text="${message}"></h1>
</div>
```

### Displaying Products on Home Page
Example:
```java
@GetMapping("/products")
public String getProducts(Model model) {
    List<Product> products = productService.getAllProducts();
    model.addAttribute("products", products);
    return "home";
}
```

## Building Pages
### Building the About Page
```java
@GetMapping("/about")
public String about() {
    return "about";
}
```

### Building the Contact Page
```java
@GetMapping("/contact")
public String contact() {
    return "contact";
}
```

## Running the Application
```sh
mvn spring-boot:run
```
Visit `http://localhost:8080` to view the application.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)