# Category Service API

## Table of Contents
- [Overview](#overview)
- [Fetching All Categories](#fetching-all-categories)
- [Adding New Categories](#adding-new-categories)
- [Setting up Category Service](#setting-up-category-service)
- [Managing IDs](#managing-ids)
- [Delete Category](#delete-category)
- [ResponseEntity Class](#responseentity-class)
- [Using ResponseEntity for all Endpoints](#using-responseentity-for-all-endpoints)
- [Update Category](#update-category)
- [@RequestMapping Annotation](#requestmapping-annotation)

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

## Overview
The **Category Service API** is a RESTful service built using **Spring Boot** that allows users to manage categories in an application. This service provides endpoints to fetch, add, update, and delete categories while ensuring proper response handling using **ResponseEntity**.

---

## Fetching All Categories
To retrieve all categories, we use the `GET` method.

```java
@GetMapping("/categories")
public ResponseEntity<List<Category>> getAllCategories() {
    List<Category> categories = categoryService.getAllCategories();
    return ResponseEntity.ok(categories);
}
```

---

## Adding New Categories
To add a new category, we use the `POST` method with `@RequestBody`.

```java
@PostMapping("/categories")
public ResponseEntity<Category> addCategory(@RequestBody Category category) {
    Category savedCategory = categoryService.addCategory(category);
    return ResponseEntity.status(HttpStatus.CREATED).body(savedCategory);
}
```

---

## Setting up Category Service
A simple **Category Service** is implemented to handle category operations.

```java
@Service
public class CategoryService {
    private final List<Category> categoryList = new ArrayList<>();

    public List<Category> getAllCategories() {
        return categoryList;
    }

    public Category addCategory(Category category) {
        categoryList.add(category);
        return category;
    }
}
```

---

## Managing IDs
Assigning and managing **unique IDs** is crucial for category operations.

```java
public class Category {
    private Long id;
    private String name;
    
    // Constructors, Getters, and Setters
}
```

---

## Delete Category
Deleting a category using `DELETE` request.

```java
@DeleteMapping("/categories/{id}")
public ResponseEntity<Void> deleteCategory(@PathVariable Long id) {
    categoryService.deleteCategory(id);
    return ResponseEntity.noContent().build();
}
```

---

## ResponseEntity Class
`ResponseEntity` is a **Spring class** used to represent HTTP responses with status codes and headers.

Example:

```java
ResponseEntity.ok(data); // Returns 200 OK
ResponseEntity.status(HttpStatus.CREATED).body(data); // Returns 201 Created
ResponseEntity.noContent().build(); // Returns 204 No Content
```

---

## Using ResponseEntity for all Endpoints
We use **ResponseEntity** in all API responses to handle HTTP status codes properly.

```java
@GetMapping("/categories/{id}")
public ResponseEntity<Category> getCategoryById(@PathVariable Long id) {
    Optional<Category> category = categoryService.getCategoryById(id);
    return category.map(ResponseEntity::ok)
                   .orElse(ResponseEntity.notFound().build());
}
```

---

## Update Category
Updating an existing category using `PUT` request.

```java
@PutMapping("/categories/{id}")
public ResponseEntity<Category> updateCategory(@PathVariable Long id, @RequestBody Category category) {
    Category updatedCategory = categoryService.updateCategory(id, category);
    return ResponseEntity.ok(updatedCategory);
}
```

---

## @RequestMapping Annotation
The `@RequestMapping` annotation is used for defining endpoint mappings.

```java
@RestController
@RequestMapping("/api")
public class CategoryController {
    // All category-related endpoints will be under /api
}
```

---

## Conclusion
This API is designed to efficiently manage categories with **RESTful principles** and **proper HTTP status codes** using `ResponseEntity`. 

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)