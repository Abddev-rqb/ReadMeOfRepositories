

# Spring Boot Validations and Custom Exceptions

## Table of Contents

- [Introduction to Validations in Spring Boot](#introduction-to-validations-in-spring-boot)
- [Making Use of Hibernate Validator](#making-use-of-hibernate-validator)
- [Making Use of @Valid](#making-use-of-valid)
- [Making Things More User Friendly](#making-things-more-user-friendly)
- [Adding More Validations](#adding-more-validations)
- [Introduction to Custom Exceptions in Spring Boot](#introduction-to-custom-exceptions-in-spring-boot)
- [Implementing ResourceNotFoundException](#implementing-resourcenotfoundexception)
- [Implement ResourceNotFoundException Services](#implement-resourcenotfoundexception-services)
- [Adding More Custom Exceptions | APIException](#adding-more-custom-exceptions--apiexception)
- [Validation For No Categories Present](#validation-for-no-categories-present)
- [Cleaning Up Controllers](#cleaning-up-controllers)

---

## Introduction to Validations in Spring Boot

Spring Boot provides built-in support for **validating user inputs** using **Hibernate Validator**, which is the reference implementation of **Jakarta Bean Validation**.

---

## Making Use of Hibernate Validator

To enable validation, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

---

## Making Use of @Valid

The `@Valid` annotation ensures that request payloads comply with the validation rules defined in the entity class.

**Example:**

```java
import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.Size;

public class CategoryDTO {
    @NotBlank(message = "Category name cannot be empty")
    @Size(min = 3, max = 50, message = "Category name must be between 3 and 50 characters")
    private String name;
}
```

Using `@Valid` in a Controller:

```java
@PostMapping("/categories")
public ResponseEntity<String> createCategory(@Valid @RequestBody CategoryDTO category) {
    return ResponseEntity.ok("Category created successfully");
}
```

---

## Making Things More User Friendly

To make validation errors more readable, we can customize the response:

```java
@ExceptionHandler(MethodArgumentNotValidException.class)
public ResponseEntity<Map<String, String>> handleValidationExceptions(MethodArgumentNotValidException ex) {
    Map<String, String> errors = new HashMap<>();
    ex.getBindingResult().getFieldErrors().forEach(error ->
        errors.put(error.getField(), error.getDefaultMessage()));
    return ResponseEntity.badRequest().body(errors);
}
```

---

## Adding More Validations

Additional annotations:

- `@Email(message = "Invalid email format")`
- `@Min(value = 18, message = "Age must be at least 18")`
- `@Pattern(regexp = "^[a-zA-Z0-9]+$", message = "Only alphanumeric characters allowed")`

---

## Introduction to Custom Exceptions in Spring Boot

Custom exceptions improve error handling by providing meaningful error messages.

---

## Implementing ResourceNotFoundException

```java
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

---

## Implement ResourceNotFoundException Services

Using `ResourceNotFoundException` in a service:

```java
public Category getCategoryById(Long id) {
    return categoryRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Category not found with id: " + id));
}
```

---

## Adding More Custom Exceptions | APIException

```java
public class APIException extends RuntimeException {
    public APIException(String message) {
        super(message);
    }
}
```

---

## Validation For No Categories Present

```java
if (categoryRepository.findAll().isEmpty()) {
    throw new APIException("No categories found in the database");
}
```

---

## Cleaning Up Controllers

Use `@ControllerAdvice` to handle exceptions globally:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

---

### Conclusion

This readMe covers essential **validation techniques** and **custom exception handling** in **Spring Boot**, making applications more secure and user-friendly.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
