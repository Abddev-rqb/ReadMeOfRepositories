# Pagination and DTO Pattern in Spring Boot

## Table of Contents
- [Pagination and How It Works](#pagination-and-how-it-works)
- [Pagination in Our Project](#pagination-in-our-project)
- [DTO Pattern](#dto-pattern)
- [Implementing DTO Pattern](#implementing-dto-pattern)
- [Model Mapper: Introduction and Usage](#model-mapper-introduction-and-usage)
- [Challenges in Implementing DTOs](#challenges-in-implementing-dtos)
  - [Challenge: Implementing DTOs for CreateCategory](#challenge-implementing-dtos-for-createcategory)
  - [Challenge: Implementing DTOs for UpdateCategory](#challenge-implementing-dtos-for-updatecategory)
  - [Challenge: Implementing DTOs for DeleteCategory](#challenge-implementing-dtos-for-deletecategory)
- [@RequestParam Annotation](#requestparam-annotation)
- [Accepting Pagination Parameters](#accepting-pagination-parameters)
- [Pageable and PageRequest](#pageable-and-pagerequest)
- [Testing Changes](#testing-changes)
- [Updating Response Structure to Include Pagination Details](#updating-response-structure-to-include-pagination-details)
- [Adding Default Values](#adding-default-values)
- [Implementing Sorting](#implementing-sorting)
- [Implementing APIResponse](#implementing-apiresponse)

---

## Pagination and How It Works
Pagination is a technique used in REST APIs to split large datasets into manageable chunks. It improves performance and optimizes resource utilization by fetching only the required records.

### Key Concepts:
- **Page**: A subset of data.
- **Size**: Number of records per page.
- **Sorting**: Ordering the results.

## Pagination in Our Project
In our project, we implement pagination using Spring Boot’s `Pageable` interface.

---

## DTO Pattern
**DTO (Data Transfer Object)** is used to transfer data between processes to avoid exposing entity models directly.

### Benefits:
- Prevents over-fetching of data
- Increases security
- Improves maintainability

## Implementing DTO Pattern
Example of a DTO:
```java
public class CategoryDTO {
    private Long id;
    private String name;
    private String description;
    // Getters and Setters
}
```

---

## Model Mapper: Introduction and Usage
`ModelMapper` is a Java library that simplifies object mapping.

### Example Usage:
```java
ModelMapper modelMapper = new ModelMapper();
CategoryDTO categoryDTO = modelMapper.map(category, CategoryDTO.class);
```

---

## Challenges in Implementing DTOs
### Challenge: Implementing DTOs for CreateCategory
```java
@PostMapping("/categories")
public ResponseEntity<CategoryDTO> createCategory(@RequestBody CategoryDTO categoryDTO) {
    Category category = modelMapper.map(categoryDTO, Category.class);
    Category savedCategory = categoryService.save(category);
    return new ResponseEntity<>(modelMapper.map(savedCategory, CategoryDTO.class), HttpStatus.CREATED);
}
```

### Challenge: Implementing DTOs for UpdateCategory
```java
@PutMapping("/categories/{id}")
public ResponseEntity<CategoryDTO> updateCategory(@PathVariable Long id, @RequestBody CategoryDTO categoryDTO) {
    Category updatedCategory = categoryService.update(id, categoryDTO);
    return ResponseEntity.ok(modelMapper.map(updatedCategory, CategoryDTO.class));
}
```

### Challenge: Implementing DTOs for DeleteCategory
```java
@DeleteMapping("/categories/{id}")
public ResponseEntity<ApiResponse> deleteCategory(@PathVariable Long id) {
    categoryService.delete(id);
    return ResponseEntity.ok(new ApiResponse("Category deleted successfully", true));
}
```

---

## @RequestParam Annotation
The `@RequestParam` annotation is used to pass pagination parameters via query parameters.

Example:
```java
@GetMapping("/categories")
public ResponseEntity<Page<CategoryDTO>> getCategories(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size) {
    Pageable pageable = PageRequest.of(page, size);
    Page<Category> categoryPage = categoryService.getAllCategories(pageable);
    Page<CategoryDTO> categoryDTOPage = categoryPage.map(category -> modelMapper.map(category, CategoryDTO.class));
    return ResponseEntity.ok(categoryDTOPage);
}
```

---

## Pageable and PageRequest
Spring Boot provides `Pageable` and `PageRequest` to handle pagination.

Example:
```java
Pageable pageable = PageRequest.of(0, 10, Sort.by("name"));
```

---

## Testing Changes
Use Postman or CURL:
```
GET /categories?page=0&size=5
```

---

## Updating Response Structure to Include Pagination Details
Wrap responses in a custom object:
```java
public class PagedResponse<T> {
    private List<T> content;
    private int page;
    private int size;
    private long totalElements;
    private int totalPages;
    private boolean last;
}
```

---

## Adding Default Values
Use default values to avoid issues when no parameters are passed.
```java
@RequestParam(defaultValue = "0") int page,
@RequestParam(defaultValue = "10") int size
```

---

## Implementing Sorting
Sorting can be applied via `Sort.by()`:
```java
Pageable pageable = PageRequest.of(page, size, Sort.by("name").ascending());
```

---

## Implementing APIResponse
Custom API response format:
```java
public class ApiResponse {
    private String message;
    private boolean success;
    
    public ApiResponse(String message, boolean success) {
        this.message = message;
        this.success = success;
    }
}
```

---

## Conclusion
This project showcases efficient data handling using Pagination, DTO, and ModelMapper in Spring Boot to create maintainable and scalable APIs.

---

