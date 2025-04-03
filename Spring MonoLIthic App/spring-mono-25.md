# Checkout Flow in a Spring Boot Monolithic Application

## Table of Contents
1. [Introduction](#introduction)
2. [Understanding Checkout for Accepting Orders](#understanding-checkout-for-accepting-orders)
3. [Project Structure](#project-structure)
4. [Setting up the Layout for Checkout Flow](#setting-up-the-layout-for-checkout-flow)
5. [Address Selection](#address-selection)
    - [Setting up the Layout](#setting-up-the-layout)
    - [Allowing users to Add Address](#allowing-users-to-add-address)
    - [Saving the User’s Address](#saving-the-users-address)
    - [Saving Cookies After Authentication in Frontend](#saving-cookies-after-authentication-in-frontend)
    - [Fetching User Addresses From Backend](#fetching-user-addresses-from-backend)
    - [Displaying User Addresses](#displaying-user-addresses)
    - [Saving Selected User Address For Checkout](#saving-selected-user-address-for-checkout)
    - [Saving the User’s Address Post Updates](#saving-the-users-address-post-updates)
    - [Allowing users to Delete Address](#allowing-users-to-delete-address)
    - [Completing the Address Flow](#completing-the-address-flow)
6. [Enhancing the Loader Screen](#enhancing-the-loader-screen)
7. [Error Handling](#error-handling)
8. [Payment Method Selection](#payment-method-selection)
    - [Redux Configuration](#redux-configuration)
    - [Setting up the Layout](#setting-up-the-layout-1)
9. [Cart Management](#cart-management)
    - [Saving User’s Cart in Backend](#saving-users-cart-in-backend)
    - [Refactor CartItemDTO](#refactor-cartitemdto)
    - [Sending Cart to Backend From Frontend](#sending-cart-to-backend-from-frontend)
10. [Getting Rid of the Strict Mode](#getting-rid-of-the-strict-mode)
11. [Order Summary](#order-summary)
12. [Price Formatting for Better UX](#price-formatting-for-better-ux)
13. [Completing the Checkout Flow](#completing-the-checkout-flow)
14. [Conclusion](#conclusion)

---

## Introduction
This document provides a detailed overview of implementing a checkout flow in a **Spring Boot Monolithic Application**. The guide covers everything from **address selection** to **payment method selection**, **cart management**, and **order summary**. It ensures a smooth e-commerce checkout process by leveraging **Spring Boot, REST APIs, Redux, and frontend integration**.

## Understanding Checkout for Accepting Orders
The checkout process involves multiple steps:
1. **User selects an address.**
2. **User selects a payment method.**
3. **Cart details are finalized and saved in the backend.**
4. **User reviews the order summary.**
5. **Order is placed and confirmed.**

This guide walks through each step with best practices for a **monolithic** architecture in **Spring Boot**.

## Project Structure
```
checkout-service/
├── src/main/java/com/example/checkout/
│   ├── controllers/
│   ├── services/
│   ├── repositories/
│   ├── models/
│   ├── dtos/
│   ├── utils/
│   ├── config/
├── src/main/resources/
│   ├── application.properties
│   ├── templates/
│   ├── static/
└── pom.xml
```

---

## Setting up the Layout for Checkout Flow
The checkout flow starts with a structured layout that guides users through the process in a clean and interactive way.

- **Backend:** Handles API calls for user details, address management, cart processing, and payment.
- **Frontend:** Manages user interactions with form validation, loaders, and address selection.

---

## Address Selection
### Setting up the Layout
- Design a UI that allows users to enter, update, and delete addresses.

### Allowing users to Add Address
- Implement REST endpoints to save user addresses.

```java
@PostMapping("/user/address")
public ResponseEntity<String> saveAddress(@RequestBody AddressDTO address) {
    addressService.saveAddress(address);
    return ResponseEntity.ok("Address saved successfully");
}
```

### Saving the User’s Address
- Persist user addresses in the database.

### Saving Cookies After Authentication in Frontend
- Store session tokens securely in cookies.

### Fetching User Addresses From Backend
```java
@GetMapping("/user/address/{userId}")
public ResponseEntity<List<AddressDTO>> getUserAddresses(@PathVariable Long userId) {
    return ResponseEntity.ok(addressService.getAddresses(userId));
}
```

### Displaying User Addresses
- Fetch and display addresses dynamically in the UI.

### Saving Selected User Address For Checkout
- Update checkout session with the selected address.

### Allowing users to Delete Address
- Provide a DELETE endpoint to remove addresses.

```java
@DeleteMapping("/user/address/{id}")
public ResponseEntity<String> deleteAddress(@PathVariable Long id) {
    addressService.deleteAddress(id);
    return ResponseEntity.ok("Address deleted successfully");
}
```

---

## Payment Method Selection
### Redux Configuration
- Use Redux for state management of payment methods.

### Setting up the Layout
- Design a UI for users to choose payment options.

---

## Cart Management
### Saving User’s Cart in Backend
```java
@PostMapping("/cart/save")
public ResponseEntity<String> saveCart(@RequestBody CartDTO cart) {
    cartService.saveCart(cart);
    return ResponseEntity.ok("Cart saved successfully");
}
```

### Sending Cart to Backend From Frontend
- Ensure the cart is properly sent and validated.

---

## Order Summary
### Formatting the Price for Better User Experience
- Implement price formatting for clarity.

### Completing the Checkout Flow
- Finalize the checkout process and confirm the order.

---

## Conclusion
This guide provided a structured approach to implementing a checkout flow in a **Spring Boot Monolithic Application**. By following these steps, developers can create an efficient, user-friendly, and scalable e-commerce checkout process.

### 📌 **Next Steps**
- Implement **Spring Security** for better authentication.
- Integrate **third-party payment gateways**.
- Optimize performance using **caching mechanisms**.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
