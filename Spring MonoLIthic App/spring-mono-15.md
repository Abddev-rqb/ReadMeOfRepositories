# Shopping Cart Module in Spring Boot (Monolithic Architecture)

## Table of Contents
- [Introduction](#introduction)
- [Cart Module Design](#cart-module-design)
- [Cart Models & Relationships](#cart-models--relationships)
- [DTOs and Repositories](#dtos-and-repositories)
- [Adding Product to the Cart](#adding-product-to-the-cart)
- [AuthUtils Class](#authutils-class)
- [Fetching Carts](#fetching-carts)
  - [Fetching All Carts](#fetching-all-carts)
  - [Fetching User's Cart](#fetching-users-cart)
- [Updating Product Quantity](#updating-product-quantity)
- [Deleting Product from Cart](#deleting-product-from-cart)
- [Handling Product Updates or Deletions](#handling-product-updates-or-deletions)
- [Testing the Module](#testing-the-module)
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
The Shopping Cart module in this project is designed using Spring Boot in a monolithic architecture. It provides core functionalities like adding products, updating quantities, removing products, and fetching user-specific cart details. This module follows best practices with DTOs, repositories, and authentication utilities.

## Cart Module Design
The cart module follows a layered approach:
1. **Controller Layer** - Handles API requests.
2. **Service Layer** - Implements business logic.
3. **Repository Layer** - Communicates with the database.
4. **DTO Layer** - Defines structured data transfer objects.
5. **Security Layer** - Manages authentication and authorization.

## Cart Models & Relationships
```java
@Entity
public class Cart {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @OneToMany(mappedBy = "cart", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<CartItem> items = new ArrayList<>();

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}
```
```java
@Entity
public class CartItem {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "cart_id")
    private Cart cart;

    @ManyToOne
    @JoinColumn(name = "product_id")
    private Product product;
    
    private int quantity;
}
```

## DTOs and Repositories
DTOs are used to transfer data efficiently:
```java
public class CartItemDTO {
    private Long productId;
    private int quantity;
}
```
Repositories:
```java
@Repository
public interface CartRepository extends JpaRepository<Cart, Long> {
    Optional<Cart> findByUserId(Long userId);
}
```

## Adding Product to the Cart
```java
public void addProductToCart(Long userId, CartItemDTO cartItemDTO) {
    Cart cart = cartRepository.findByUserId(userId).orElse(new Cart(user));
    Product product = productRepository.findById(cartItemDTO.getProductId()).orElseThrow();
    CartItem cartItem = new CartItem(cart, product, cartItemDTO.getQuantity());
    cart.getItems().add(cartItem);
    cartRepository.save(cart);
}
```

## AuthUtils Class
Handles authentication-related operations:
```java
@Component
public class AuthUtils {
    public Long getAuthenticatedUserId() {
        return SecurityContextHolder.getContext().getAuthentication().getPrincipal();
    }
}
```

## Fetching Carts
### Fetching All Carts
```java
public List<Cart> getAllCarts() {
    return cartRepository.findAll();
}
```
### Fetching User's Cart
```java
public Cart getUserCart(Long userId) {
    return cartRepository.findByUserId(userId).orElseThrow();
}
```

## Updating Product Quantity
```java
public void updateCartItem(Long userId, Long productId, int newQuantity) {
    Cart cart = cartRepository.findByUserId(userId).orElseThrow();
    cart.getItems().stream()
        .filter(item -> item.getProduct().getId().equals(productId))
        .forEach(item -> item.setQuantity(newQuantity));
    cartRepository.save(cart);
}
```

## Deleting Product from Cart
```java
public void removeProductFromCart(Long userId, Long productId) {
    Cart cart = cartRepository.findByUserId(userId).orElseThrow();
    cart.getItems().removeIf(item -> item.getProduct().getId().equals(productId));
    cartRepository.save(cart);
}
```

## Handling Product Updates or Deletions
If a product is deleted, it must be removed from all carts:
```java
@Transactional
public void handleProductDeletion(Long productId) {
    cartItemRepository.deleteByProductId(productId);
}
```

## Testing the Module
JUnit & MockMvc are used for testing:
```java
@Test
public void testAddProductToCart() throws Exception {
    mockMvc.perform(post("/cart/add")
        .content(asJsonString(new CartItemDTO(1L, 2)))
        .contentType(MediaType.APPLICATION_JSON))
        .andExpect(status().isOk());
}
```

## Conclusion
This Shopping Cart module provides essential functionalities in a monolithic Spring Boot application. It ensures efficient data handling, security, and proper testing strategies. This project is scalable and can be further enhanced with caching, event-driven processing, or microservices-based refactoring.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
