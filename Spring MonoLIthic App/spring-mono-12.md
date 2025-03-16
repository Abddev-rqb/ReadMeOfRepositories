# Product Module Documentation

## Table of Contents
- [Introduction](#introduction)
- [Setting Up Product Module](#setting-up-product-module)
- [Setting Up DTOs for Products](#setting-up-dtos-for-products)
- [Saving Products to a Category](#saving-products-to-a-category)
- [Getting All the Products](#getting-all-the-products)
- [Get Products by Category](#get-products-by-category)
- [Get Products by Keyword](#get-products-by-keyword)
- [Update Product](#update-product)
- [Delete Product](#delete-product)
- [Using Product DTO in Controllers](#using-product-dto-in-controllers)
- [Update Product Image](#update-product-image)
- [Making Use of FileService and application.properties](#making-use-of-fileservice-and-applicationproperties)
- [Adding Validations and Custom Exceptions](#adding-validations-and-custom-exceptions)
- [Implementing Pagination and Sorting](#implementing-pagination-and-sorting)
- [Conclusion](#conclusion)

---

## Introduction
The **Product Module** is a core part of any e-commerce platform. This module handles product management functionalities such as creating, updating, deleting, and retrieving products. It also supports image handling, validations, and search functionalities.

---

## Setting Up Product Module
To set up the product module, create a Spring Boot application with dependencies:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

---

## Setting Up DTOs for Products
Data Transfer Objects (DTOs) help in decoupling the entity from API response models.
```java
public class ProductDTO {
    private Long id;
    private String name;
    private String description;
    private Double price;
    private String category;
    private String imageUrl;
}
```

---

## Saving Products to a Category
```java
@PostMapping("/category/{categoryId}/products")
public ResponseEntity<ProductDTO> createProduct(@PathVariable Long categoryId, @RequestBody ProductDTO productDTO) {
    ProductDTO createdProduct = productService.addProductToCategory(categoryId, productDTO);
    return new ResponseEntity<>(createdProduct, HttpStatus.CREATED);
}
```

---

## Getting All the Products
```java
@GetMapping("/products")
public ResponseEntity<List<ProductDTO>> getAllProducts() {
    return ResponseEntity.ok(productService.getAllProducts());
}
```

---

## Get Products by Category
```java
@GetMapping("/category/{categoryId}/products")
public ResponseEntity<List<ProductDTO>> getProductsByCategory(@PathVariable Long categoryId) {
    return ResponseEntity.ok(productService.getProductsByCategory(categoryId));
}
```

---

## Get Products by Keyword
```java
@GetMapping("/products/search")
public ResponseEntity<List<ProductDTO>> searchProducts(@RequestParam String keyword) {
    return ResponseEntity.ok(productService.searchProducts(keyword));
}
```

---

## Update Product
```java
@PutMapping("/products/{id}")
public ResponseEntity<ProductDTO> updateProduct(@PathVariable Long id, @RequestBody ProductDTO productDTO) {
    return ResponseEntity.ok(productService.updateProduct(id, productDTO));
}
```

---

## Delete Product
```java
@DeleteMapping("/products/{id}")
public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
    productService.deleteProduct(id);
    return ResponseEntity.noContent().build();
}
```

---

## Using Product DTO in Controllers
The DTO is used to ensure clean API responses and avoid exposing the entity directly.

---

## Update Product Image
```java
@PutMapping("/products/{id}/image")
public ResponseEntity<String> updateProductImage(@PathVariable Long id, @RequestParam("file") MultipartFile file) {
    return ResponseEntity.ok(productService.updateProductImage(id, file));
}
```

---

## Making Use of FileService and application.properties
Store images securely and configure paths in `application.properties`:
```properties
file.upload-dir=./uploads
```

---

## Adding Validations and Custom Exceptions
Ensure data integrity using validation annotations:
```java
public class ProductDTO {
    @NotBlank(message = "Product name is required")
    private String name;

    @Min(value = 1, message = "Price must be greater than zero")
    private Double price;
}
```

---

## Implementing Pagination and Sorting
```java
@GetMapping("/products/paged")
public ResponseEntity<Page<ProductDTO>> getPagedProducts(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(defaultValue = "id") String sortBy) {
    return ResponseEntity.ok(productService.getPagedProducts(page, size, sortBy));
}
```

---

## Conclusion
This module provides a robust way to manage products with proper structuring, validation, and security. It ensures scalability and maintainability in an enterprise-level e-commerce application.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
