

# Shopping Cart in Spring Boot (Monolithic Architecture)

## Table of Contents
- [Introduction](#introduction)
- [Understanding Shopping Carts](#understanding-shopping-carts)
- [Building Add to Cart Functionality](#building-add-to-cart-functionality)
- [Building Cart Page](#building-cart-page)
- [Displaying Cart Content](#displaying-cart-content)
- [Allowing Users to Increase Quantity From Cart](#allowing-users-to-increase-quantity-from-cart)
- [Allowing Users to Decrease Quantity From Cart](#allowing-users-to-decrease-quantity-from-cart)
- [Allowing Users to Remove Items From Cart](#allowing-users-to-remove-items-from-cart)
- [Setting Up Empty Cart Page](#setting-up-empty-cart-page)
- [Formatting Cart Data to Display](#formatting-cart-data-to-display)
- [Building a Reactive Cart Badge for the Navbar](#building-a-reactive-cart-badge-for-the-navbar)
- [Fixing Subtotal Price in Shopping Cart](#fixing-subtotal-price-in-shopping-cart)
- [Conclusion](#conclusion)

## Introduction
This project demonstrates a fully functional shopping cart system built using **Spring Boot (Monolithic Architecture)**. It allows users to add products to a cart, manage their quantities, remove items, and view order summaries before checkout. 

## Understanding Shopping Carts
A shopping cart is a temporary storage system that enables users to select products before purchasing. It typically includes:
- Product details
- Quantity management
- Subtotal and total price calculation
- Checkout process integration

## Building Add to Cart Functionality
- Users can add products to the cart using a REST API or UI action.
- Spring Boot handles cart persistence using session-based storage or a database.
- Example API endpoint:
  ```java
  @PostMapping("/cart/add")
  public ResponseEntity<String> addToCart(@RequestParam Long productId) {
      cartService.addItem(productId);
      return ResponseEntity.ok("Item added to cart");
  }
  ```

## Building Cart Page
- A dedicated `/cart` page displays all selected items.
- Fetch cart contents from the database or session storage.
- Example Thymeleaf template snippet:
  ```html
  <table>
      <tr th:each="item : ${cartItems}">
          <td th:text="${item.product.name}"></td>
          <td th:text="${item.quantity}"></td>
          <td th:text="${item.price}"></td>
      </tr>
  </table>
  ```

## Displaying Cart Content
- Fetch cart details using a service layer:
  ```java
  public List<CartItem> getCartItems() {
      return cartRepository.findAll();
  }
  ```
- Display items dynamically in the UI.

## Allowing Users to Increase Quantity From Cart
- Implement an endpoint to increase item quantity:
  ```java
  @PostMapping("/cart/increase")
  public ResponseEntity<String> increaseQuantity(@RequestParam Long itemId) {
      cartService.increaseItemQuantity(itemId);
      return ResponseEntity.ok("Quantity increased");
  }
  ```

## Allowing Users to Decrease Quantity From Cart
- Implement a decrease quantity functionality, ensuring a minimum of 1 item:
  ```java
  @PostMapping("/cart/decrease")
  public ResponseEntity<String> decreaseQuantity(@RequestParam Long itemId) {
      cartService.decreaseItemQuantity(itemId);
      return ResponseEntity.ok("Quantity decreased");
  }
  ```

## Allowing Users to Remove Items From Cart
- Provide an option to remove items from the cart:
  ```java
  @DeleteMapping("/cart/remove")
  public ResponseEntity<String> removeFromCart(@RequestParam Long itemId) {
      cartService.removeItem(itemId);
      return ResponseEntity.ok("Item removed");
  }
  ```

## Setting Up Empty Cart Page
- If no items exist, show an empty cart message:
  ```html
  <p th:if="${#lists.isEmpty(cartItems)}">Your cart is empty.</p>
  ```

## Formatting Cart Data to Display
- Ensure a structured table with clear item names, prices, and totals.
- Format prices using Java's `DecimalFormat`.
  ```java
  DecimalFormat df = new DecimalFormat("0.00");
  String formattedPrice = df.format(item.getPrice());
  ```

## Building a Reactive Cart Badge for the Navbar
- Display the cart item count dynamically.
- Use WebSocket or AJAX polling to update the cart icon dynamically.
  ```html
  <span id="cart-badge" th:text="${cartItemCount}"></span>
  ```
  ```javascript
  setInterval(() => {
      fetch('/cart/count').then(res => res.text()).then(count => {
          document.getElementById('cart-badge').textContent = count;
      });
  }, 5000);
  ```

## Fixing Subtotal Price in Shopping Cart
- Calculate subtotal per item dynamically:
  ```java
  public double getSubtotal() {
      return cartItems.stream()
          .mapToDouble(item -> item.getPrice() * item.getQuantity())
          .sum();
  }
  ```
- Display the subtotal in the cart page:
  ```html
  <p>Total: <span th:text="${cartSubtotal}"></span></p>
  ```

## Conclusion
This Spring Boot monolithic shopping cart system provides a fully functional backend for managing a shopping experience. Future improvements include integrating payment gateways and moving towards a microservices architecture for better scalability.

---
### 🛠️ Built With
- **Spring Boot** - Backend framework
- **Thymeleaf** - Frontend templating engine
- **Spring Data JPA** - Database management
- **H2/MySQL** - Database
- **AJAX & WebSockets** - Real-time cart updates

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)