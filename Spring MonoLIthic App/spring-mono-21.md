

# Structured, Scalable Product Storefront with Spring Boot

## Table of Contents

1. [Introduction](#introduction)
2. [Setting up the Structure](#setting-up-the-structure)
3. [Product Component and Layout](#product-component-and-layout)
4. [Building and Styling the Product Card](#building-and-styling-the-product-card)
5. [Product View with Modal](#product-view-with-modal)
6. [Role of Redux in State Management](#role-of-redux-in-state-management)
7. [Setting Up Redux for Global State](#setting-up-redux-for-global-state)
8. [Configuring Axios for API Calls](#configuring-axios-for-api-calls)
9. [Fetching Products from API](#fetching-products-from-api)
10. [Fixing CORS Issues](#fixing-cors-issues)
11. [Handling Images in Frontend](#handling-images-in-frontend)
12. [Loaders and Error Handling](#loaders-and-error-handling)
13. [Product Filtering Functionality](#product-filtering-functionality)
14. [Product Filter Interface](#product-filter-interface)
15. [Adding Life to Product Filters](#adding-life-to-product-filters)
16. [Filtering with URL Parameters](#filtering-with-url-parameters)
17. [Backend Filtering Logic](#backend-filtering-logic)
18. [Testing Filters](#testing-filters)
19. [Dynamic Categories](#dynamic-categories)
20. [Pagination for Products](#pagination-for-products)
21. [Reusable Utilities](#reusable-utilities)
22. [Project Organization & Testing](#project-organization--testing)
23. [Conclusion](#conclusion)

---

## Introduction

This project is a structured, scalable product storefront built using **Spring Boot** in a monolithic architecture. It follows best practices for backend API development, frontend integration, state management, and UI components to deliver an efficient e-commerce platform.

## Setting up the Structure

- **Spring Boot Monolith:** The entire application, including authentication, product management, and UI, is handled in a single codebase.
- **Technology Stack:**
  - Backend: Spring Boot, Spring Security, JPA, Hibernate
  - Frontend: React with Redux for state management
  - Database: PostgreSQL/MySQL
  - API: RESTful endpoints with JWT authentication

## Product Component and Layout

- Created a `ProductComponent` in React to structure the product listing page.
- Uses **CSS modules** and **Bootstrap** for styling.

## Building and Styling the Product Card

- Developed `ProductCard` as a reusable React component.
- Includes product image, name, price, and action buttons.

## Product View with Modal

- Clicking on a product opens a **modal** displaying details fetched from the backend.
- Implemented using **React Bootstrap**.

## Role of Redux in State Management

- Redux stores and manages product lists, filters, and cart data globally.
- Enhances scalability by separating concerns.

## Setting Up Redux for Global State

- Configured **Redux store** with slices for products and filters.
- Uses **Redux Toolkit** for simplified state management.

## Configuring Axios for API Calls

- **Custom Axios instance** set up for API communication.
- Base URL and authentication headers are managed globally.

## Fetching Products from API

- Products are retrieved from the **Spring Boot API** using **RESTful endpoints**.
- Uses **Spring Data JPA** for database interaction.

## Fixing CORS Issues

- Configured **Spring Boot CORS policy** to allow frontend requests.
- Example:
  ```java
  @Bean
  public WebMvcConfigurer corsConfigurer() {
      return new WebMvcConfigurer() {
          @Override
          public void addCorsMappings(CorsRegistry registry) {
              registry.addMapping("/**").allowedOrigins("http://localhost:3000");
          }
      };
  }
  ```

## Handling Images in Frontend

- Constructs image URLs dynamically using **Spring Boot static resource mapping**.
- Example:
  ```java
  @Configuration
  public class StaticResourceConfig implements WebMvcConfigurer {
      @Override
      public void addResourceHandlers(ResourceHandlerRegistry registry) {
          registry.addResourceHandler("/images/**")
              .addResourceLocations("file:src/main/resources/static/images/");
      }
  }
  ```

## Loaders and Error Handling

- Implemented **React Spinners** for better UI experience.
- Centralized error handling using a global Redux state.

## Product Filtering Functionality

- Filters products based on **categories, price, and keywords**.
- Backend uses **Spring Data JPA Specification API**.

## Filtering with URL Parameters

- Uses **React Router** to persist filters in the URL.

## Backend Filtering Logic

```java
@Query("SELECT p FROM Product p WHERE p.category = :category")
List<Product> findByCategory(@Param("category") String category);
```

## Pagination for Products

- Implemented **Spring Boot Pagination**.
- Example:
  ```java
  Page<Product> findAll(Pageable pageable);
  ```

## Reusable Utilities

- **Text Truncation:**
  ```js
  export const truncateText = (text, length) =>
    text.length > length ? text.substring(0, length) + "..." : text;
  ```

- **Price Formatting:**
  ```js
  export const formatPrice = (price) => `$${price.toFixed(2)}`;
  ```

## Project Organization & Testing

- **Modular folder structure** for maintainability.
- **Unit tests** using **JUnit and Mockito**.

## Conclusion

This structured, scalable storefront ensures smooth development, easy maintenance, and high performance while following best practices in **Spring Boot Monolithic architecture**. The integration of Redux with React, efficient API handling with Axios, and well-optimized backend queries make this a robust e-commerce solution.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)