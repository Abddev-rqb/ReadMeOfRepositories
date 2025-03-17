# Address Management in Spring Boot (Monolithic Architecture)

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Setting up DTO and Repository](#setting-up-dto-and-repository)
- [Creating Addresses](#creating-addresses)
- [Getting Addresses](#getting-addresses)
- [Getting Specific Address](#getting-specific-address)
- [Getting Address By User](#getting-address-by-user)
- [Updating Address](#updating-address)
- [Deleting Address](#deleting-address)
- [Conclusion](#conclusion)

## Introduction

This project is a Spring Boot-based monolithic application that manages addresses. It demonstrates how to implement Data Transfer Objects (DTOs), repositories, and RESTful endpoints for CRUD operations.

## Prerequisites

- Java 17+
- Spring Boot 3+
- Maven or Gradle
- H2/PostgreSQL/MySQL database
- IDE (IntelliJ, VS Code, Eclipse, etc.)

## Project Structure
```
/AddressManagement
│── src/main/java/com/example/addressmanagement
│   ├── controller
│   │   ├── AddressController.java
│   ├── dto
│   │   ├── AddressDTO.java
│   ├── entity
│   │   ├── Address.java
│   ├── repository
│   │   ├── AddressRepository.java
│   ├── service
│   │   ├── AddressService.java
│   ├── AddressManagementApplication.java
│── src/main/resources
│   ├── application.properties
│── pom.xml
```

## Setting up DTO and Repository

**DTO (Data Transfer Object) - `AddressDTO.java`**
```java
package com.example.addressmanagement.dto;

import lombok.Data;

@Data
public class AddressDTO {
    private Long id;
    private String street;
    private String city;
    private String state;
    private String zipCode;
    private Long userId;
}
```

**Repository - `AddressRepository.java`**
```java
package com.example.addressmanagement.repository;

import com.example.addressmanagement.entity.Address;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public interface AddressRepository extends JpaRepository<Address, Long> {
    List<Address> findByUserId(Long userId);
}
```

## Creating Addresses

**POST /api/addresses**
```java
@PostMapping
public ResponseEntity<Address> createAddress(@RequestBody AddressDTO addressDTO) {
    Address address = addressService.createAddress(addressDTO);
    return ResponseEntity.status(HttpStatus.CREATED).body(address);
}
```

## Getting Addresses

**GET /api/addresses**
```java
@GetMapping
public List<Address> getAllAddresses() {
    return addressService.getAllAddresses();
}
```

## Getting Specific Address

**GET /api/addresses/{id}**
```java
@GetMapping("/{id}")
public ResponseEntity<Address> getAddressById(@PathVariable Long id) {
    return ResponseEntity.ok(addressService.getAddressById(id));
}
```

## Getting Address By User

**GET /api/addresses/user/{userId}**
```java
@GetMapping("/user/{userId}")
public List<Address> getAddressesByUserId(@PathVariable Long userId) {
    return addressService.getAddressesByUserId(userId);
}
```

## Updating Address

**PUT /api/addresses/{id}**
```java
@PutMapping("/{id}")
public ResponseEntity<Address> updateAddress(@PathVariable Long id, @RequestBody AddressDTO addressDTO) {
    Address updatedAddress = addressService.updateAddress(id, addressDTO);
    return ResponseEntity.ok(updatedAddress);
}
```

## Deleting Address

**DELETE /api/addresses/{id}**
```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteAddress(@PathVariable Long id) {
    addressService.deleteAddress(id);
    return ResponseEntity.noContent().build();
}
```

## Conclusion
This project demonstrates the essential CRUD operations for managing addresses in a Spring Boot monolithic architecture. You can expand it further by adding authentication, validation, and database migrations for production use.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)

