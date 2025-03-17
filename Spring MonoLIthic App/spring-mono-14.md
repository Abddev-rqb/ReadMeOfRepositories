# Spring Boot JWT Authentication

## Table of Contents

- [Introduction](#introduction)
- [Configuring Project to Work with JWT](#configuring-project-to-work-with-jwt)
- [Understanding UserDetails and UserDetailsService](#understanding-userdetails-and-userdetailsservice)
- [Custom UserDetails](#custom-userdetails)
- [Custom UserDetailService](#custom-userdetailservice)
- [Creating UserRepository](#creating-userrepository)
- [Managing Security Configuration](#managing-security-configuration)
- [Overview of Authentication Controller](#overview-of-authentication-controller)
- [Signin Endpoint](#signin-endpoint)
- [Signup Endpoint](#signup-endpoint)
- [Creating RoleRepository](#creating-rolerepository)
- [Loose Ends](#loose-ends)
- [Testing Changes](#testing-changes)
- [Cookie-Based Authentication in JWT](#cookie-based-authentication-in-jwt)
- [Modifying Code to Implement Cookie-Based Auth](#modifying-code-to-implement-cookie-based-auth)
- [Getting Authenticated User Details](#getting-authenticated-user-details)
- [Signout Endpoint](#signout-endpoint)

---

## Technology Stack
- Java 17
- Spring Boot 3.x
- Spring Data JPA (Hibernate)
- Spring Security 6.x
- Spring Security (JWT Authentication)
- MySQL Database
- Lombok
- Postman (for testing)
- Maven

---

## Introduction
This project demonstrates how to implement JSON Web Token (JWT) authentication in a Spring Boot monolithic application. It covers user authentication, role-based access control, security configuration, and cookie-based authentication.

## Configuring Project to Work with JWT
1. Add dependencies in `pom.xml`:
```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.11.5</version>
</dependency>
```
2. Configure properties in `application.properties`:
```properties
jwt.secret=mysecretkey
jwt.expirationMs=86400000
```

## Understanding UserDetails and UserDetailsService
- `UserDetails` represents the user information.
- `UserDetailsService` loads user-specific data for authentication.

## Custom UserDetails
Define a `CustomUserDetails` class implementing `UserDetails`:
```java
public class CustomUserDetails implements UserDetails {
    private String username;
    private String password;
    private Collection<? extends GrantedAuthority> authorities;
    
    // Constructor & overridden methods here
}
```

## Custom UserDetailService
Implement `UserDetailsService` to fetch user details from DB:
```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
    @Autowired
    private UserRepository userRepository;
    
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User not found"));
        return new CustomUserDetails(user);
    }
}
```

## Creating UserRepository
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}
```

## Managing Security Configuration
Configure Spring Security to use JWT authentication:
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Autowired
    private JwtAuthenticationFilter jwtAuthenticationFilter;

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeHttpRequests()
            .requestMatchers("/auth/**").permitAll()
            .anyRequest().authenticated()
            .and()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
        
        http.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);
        return http.build();
    }
}
```

## Overview of Authentication Controller
Handles user authentication endpoints.

## Signin Endpoint
```java
@PostMapping("/signin")
public ResponseEntity<?> authenticateUser(@RequestBody LoginRequest loginRequest) {
    Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(loginRequest.getUsername(), loginRequest.getPassword()));
    String jwt = jwtUtils.generateJwtToken(authentication);
    return ResponseEntity.ok(new JwtResponse(jwt));
}
```

## Signup Endpoint
```java
@PostMapping("/signup")
public ResponseEntity<?> registerUser(@RequestBody SignupRequest signUpRequest) {
    User user = new User(signUpRequest.getUsername(), passwordEncoder.encode(signUpRequest.getPassword()));
    userRepository.save(user);
    return ResponseEntity.ok("User registered successfully");
}
```

## Creating RoleRepository
```java
@Repository
public interface RoleRepository extends JpaRepository<Role, Long> {
    Optional<Role> findByName(String name);
}
```

## Loose Ends
- Add exception handling
- Implement user role validation

## Testing Changes
Use Postman to test authentication endpoints:
- `POST /auth/signup`
- `POST /auth/signin`

## Cookie-Based Authentication in JWT
Modify JWT to be stored in a cookie instead of header.

## Modifying Code to Implement Cookie-Based Auth
```java
ResponseCookie jwtCookie = ResponseCookie.from("jwt", jwt)
        .httpOnly(true)
        .path("/")
        .maxAge(86400)
        .build();
response.addHeader(HttpHeaders.SET_COOKIE, jwtCookie.toString());
```

## Getting Authenticated User Details
```java
@GetMapping("/user")
public ResponseEntity<UserDetails> getUserDetails(Authentication authentication) {
    return ResponseEntity.ok((UserDetails) authentication.getPrincipal());
}
```

## Signout Endpoint
```java
@PostMapping("/signout")
public ResponseEntity<?> logoutUser(HttpServletResponse response) {
    ResponseCookie cookie = ResponseCookie.from("jwt", "").maxAge(0).httpOnly(true).path("/").build();
    response.addHeader(HttpHeaders.SET_COOKIE, cookie.toString());
    return ResponseEntity.ok("User signed out successfully");
}
```

---

## Conclusion
This project covers JWT authentication with Spring Boot in a monolithic architecture. It includes token generation, user authentication, security configuration, and cookie-based authentication to enhance security.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)