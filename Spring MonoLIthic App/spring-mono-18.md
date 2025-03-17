

# Order Management System

## Table of Contents
- [Introduction](#introduction)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Setting Up the Models for Order Management](#setting-up-the-models-for-order-management)
- [Managing Payments](#managing-payments)
- [Setting Up DTOs](#setting-up-dtos)
- [Setting Up Repositories to Manage Orders](#setting-up-repositories-to-manage-orders)
- [Managing Order Placements](#managing-order-placements)
- [Managing Order Placements | Service Layer](#managing-order-placements--service-layer)
- [Testing Order Placement](#testing-order-placement)
- [Fixing Quantity in All Carts API](#fixing-quantity-in-all-carts-api)
- [Running the Application](#running-the-application)
- [Contributing](#contributing)
- [License](#license)

---

## Introduction
The **Order Management System** is a Spring Boot monolithic application that handles order processing, payment management, and cart management efficiently. This project is designed with a modular structure, making it easy to maintain and extend.

---

## Technology Stack
- Java 17
- Spring Boot 3.x
- Spring Data JPA (Hibernate)
- Spring Security (JWT Authentication)
- MySQL Database
- Lombok
- JUnit & Mockito (for testing)
- Maven

---

## Project Structure
```
order-management/
├── src/main/java/com/example/order/
│   ├── model/              # Entity Models
│   ├── dto/                # Data Transfer Objects
│   ├── repository/         # JPA Repositories
│   ├── service/            # Service Layer
│   ├── controller/         # REST Controllers
│   ├── config/             # Configuration Files
│   ├── exception/          # Custom Exceptions
│   ├── security/           # Security Configurations
│   ├── OrderManagementApplication.java
├── src/test/java/com/example/order/ # Unit and Integration Tests
├── pom.xml                  # Maven Dependencies
├── README.md                # Project Documentation
```

---

## Setting Up the Models for Order Management
```java
@Entity
@Table(name = "orders")
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String customerName;
    
    @Column(nullable = false)
    private Double totalAmount;

    @Enumerated(EnumType.STRING)
    private OrderStatus status;

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
    private List<OrderItem> items;

    // Getters and Setters
}
```

---

## Managing Payments
```java
@Service
public class PaymentService {
    public Payment processPayment(Order order, PaymentDetails details) {
        // Payment processing logic
        return new Payment(order, PaymentStatus.SUCCESS);
    }
}
```

---

## Setting Up DTOs
```java
public record OrderDTO(Long id, String customerName, Double totalAmount) {}
```

---

## Setting Up Repositories to Manage Orders
```java
@Repository
public interface OrderRepository extends JpaRepository<Order, Long> {
    List<Order> findByStatus(OrderStatus status);
}
```

---

## Managing Order Placements
```java
@RestController
@RequestMapping("/orders")
public class OrderController {
    @Autowired private OrderService orderService;
    
    @PostMapping
    public ResponseEntity<Order> placeOrder(@RequestBody OrderDTO orderDTO) {
        return ResponseEntity.ok(orderService.placeOrder(orderDTO));
    }
}
```

---

## Managing Order Placements | Service Layer
```java
@Service
public class OrderService {
    @Autowired private OrderRepository orderRepository;
    
    public Order placeOrder(OrderDTO orderDTO) {
        Order order = new Order();
        order.setCustomerName(orderDTO.customerName());
        order.setTotalAmount(orderDTO.totalAmount());
        order.setStatus(OrderStatus.PENDING);
        return orderRepository.save(order);
    }
}
```

---

## Testing Order Placement
```java
@SpringBootTest
public class OrderServiceTest {
    @Autowired private OrderService orderService;
    
    @Test
    public void testPlaceOrder() {
        OrderDTO dto = new OrderDTO(null, "John Doe", 150.00);
        Order order = orderService.placeOrder(dto);
        assertEquals("John Doe", order.getCustomerName());
    }
}
```

---

## Fixing Quantity in All Carts API
```java
@PutMapping("/cart/{cartId}/update-quantity")
public ResponseEntity<Cart> updateCartQuantity(@PathVariable Long cartId, @RequestBody CartUpdateRequest request) {
    return ResponseEntity.ok(cartService.updateQuantity(cartId, request));
}
```

---

## Running the Application
```sh
mvn clean install
mvn spring-boot:run
```

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)