# Social Media Platform - Working with Multiple Entities & Relationships

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [One-to-One Relationship](#one-to-one-relationship)
   - [Bi-directional Mapping in One-To-One Relationship](#bi-directional-mapping-in-one-to-one-relationship)
4. [One-to-Many and Many-to-One Relationship](#one-to-many-and-many-to-one-relationship)
5. [Many-to-Many Relationship](#many-to-many-relationship)
6. [Setting Up APIs](#setting-up-apis)
7. [Circular References & @JsonIgnore](#circular-references--using-jsonignore)
8. [Cascading](#cascading)
   - [CascadeType.ALL](#cascadetypeall)
   - [CascadeType.PERSIST](#cascadetypepersist)
   - [CascadeType.REMOVE](#cascadetyperemove)
   - [Multiple Cascading at Once](#multiple-cascading-at-once)
9. [Fetch Types](#fetch-types)
   - [Eager Fetch Type](#eager-fetch-type)
   - [Lazy Fetch Type](#lazy-fetch-type)
10. [Common Errors](#common-errors)
    - [org.hibernate.StaleObjectStateException](#error-resolving-orghibernatestaleobjectstateexception)

---

## Introduction
In this project, we will explore entity relationships in a social media platform using Spring Boot and Hibernate. We will cover different types of relationships and cascading strategies, along with handling circular references in JSON responses.

## Setting Up the Project
1. Create a Spring Boot project with dependencies:
   - Spring Web
   - Spring Data JPA
   - MySQL Driver
   - Lombok
   - Hibernate Validator
2. Configure `application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/social_media_db
   spring.datasource.username=root
   spring.datasource.password=password
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```

## One-to-One Relationship
A one-to-one relationship connects two entities, where each entity has a single corresponding entity.

### Bi-directional Mapping in One-To-One Relationship
```java
@Entity
public class Profile {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String bio;
    
    @OneToOne(mappedBy = "profile", cascade = CascadeType.ALL)
    private User user;
}

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String username;
    
    @OneToOne
    @JoinColumn(name = "profile_id")
    private Profile profile;
}
```

## One-to-Many and Many-to-One Relationship
One user can have multiple posts, and each post belongs to one user.
```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String username;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Post> posts;
}

@Entity
public class Post {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String content;
    
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}
```

## Many-to-Many Relationship
Users can follow multiple users, and vice versa.
```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String username;
    
    @ManyToMany
    @JoinTable(
        name = "user_followers",
        joinColumns = @JoinColumn(name = "user_id"),
        inverseJoinColumns = @JoinColumn(name = "follower_id")
    )
    private List<User> followers;
}
```

## Setting Up APIs
```java
@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserRepository userRepository;
    
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
    
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userRepository.findById(id).orElseThrow();
    }
}
```

## Circular References & Using @JsonIgnore
To prevent infinite recursion when returning JSON:
```java
@Entity
public class User {
    @OneToOne(mappedBy = "user")
    @JsonIgnore
    private Profile profile;
}
```

## Cascading
### CascadeType.ALL
Applies all cascade operations:
```java
@OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
private List<Post> posts;
```

### CascadeType.PERSIST
Saves child entities when parent is saved:
```java
@OneToOne(cascade = CascadeType.PERSIST)
private Profile profile;
```

### CascadeType.REMOVE
Deletes child entities when parent is deleted:
```java
@OneToMany(mappedBy = "user", cascade = CascadeType.REMOVE)
private List<Post> posts;
```

### Multiple Cascading at Once
```java
@OneToOne(cascade = {CascadeType.PERSIST, CascadeType.REMOVE})
private Profile profile;
```

## Fetch Types
### Eager Fetch Type
Loads related entities immediately.
```java
@OneToOne(fetch = FetchType.EAGER)
private Profile profile;
```

### Lazy Fetch Type
Loads related entities only when accessed.
```java
@OneToOne(fetch = FetchType.LAZY)
private Profile profile;
```

## Common Errors
### ERROR Resolving: org.hibernate.StaleObjectStateException
Occurs when multiple transactions update the same entity.
#### Solution:
- Use `@Version` for optimistic locking.
```java
@Version
private Long version;
```
- Ensure transactions are handled properly.

---

## Conclusion
This project demonstrates how to model entity relationships in a social media platform using Spring Boot and Hibernate. It covers relationships, cascading, fetch types, and common errors. The API setup ensures structured data retrieval while handling circular references efficiently.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)