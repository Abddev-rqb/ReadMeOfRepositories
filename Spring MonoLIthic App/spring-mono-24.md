

# Authentication in a Spring Boot Monolithic Application

## Table of Contents
1. [Understanding Authentication](#understanding-authentication)
2. [Setting up Redux For User Authentication](#setting-up-redux-for-user-authentication)
3. [Setting up InputField Component](#setting-up-inputfield-component)
4. [Setting up Login Interface](#setting-up-login-interface)
5. [Authenticating Users with Backend](#authenticating-users-with-backend)
6. [Updating NavBar On Authentication](#updating-navbar-on-authentication)
7. [Displaying User Menu If Authenticated](#displaying-user-menu-if-authenticated)
8. [Adding Backdrop To Improve User Experience](#adding-backdrop-to-improve-user-experience)
9. [Implementing Private Routes for Authentication](#implementing-private-routes-for-authentication)
10. [User Registration: Setting up the layout](#user-registration-setting-up-the-layout)
11. [User Registration: Building the Flow](#user-registration-building-the-flow)
12. [Implementing LogOut Functionality](#implementing-logout-functionality)
13. [Improving User Experience with Spinners](#improving-user-experience-with-spinners)
14. [Redirecting User to Home After Login](#redirecting-user-to-home-after-login)

## Understanding Authentication
Authentication is the process of verifying the identity of a user. In a monolithic Spring Boot application, authentication is typically implemented using Spring Security with JWT (JSON Web Token) or session-based authentication.

## Setting up Redux For User Authentication
In a React front-end, Redux is used to manage authentication state globally. Actions and reducers help in storing user authentication status, login/logout actions, and session persistence.

## Setting up InputField Component
A reusable `InputField` component ensures a consistent input UI across the application. It accepts props for label, type, placeholder, and validation.

## Setting up Login Interface
The login interface consists of a form where users can enter their credentials. It integrates with Redux for authentication and handles form validation.

## Authenticating Users with Backend
Spring Boot handles authentication by validating user credentials against a database using `UserDetailsService` and generating JWT tokens upon successful login.

### Example Authentication Controller (Spring Boot):
```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {

    @Autowired
    private AuthenticationService authenticationService;

    @PostMapping("/login")
    public ResponseEntity<AuthResponse> login(@RequestBody AuthRequest request) {
        return ResponseEntity.ok(authenticationService.authenticate(request));
    }
}
```

## Updating NavBar On Authentication
The navigation bar dynamically updates based on the user's authentication status. If the user is logged in, a profile menu appears; otherwise, login/register options are displayed.

## Displaying User Menu If Authenticated
Once authenticated, users should see their profile picture, name, and a logout button.

## Adding Backdrop To Improve User Experience
A backdrop UI enhances UX by preventing multiple actions when authentication requests are in progress.

## Implementing Private Routes for Authentication
Private routes ensure that only authenticated users can access certain pages. In React, this is typically implemented using a higher-order component (HOC) or React Router's `Navigate`.

### Example Private Route in React:
```jsx
const PrivateRoute = ({ children }) => {
    const user = useSelector((state) => state.auth.user);
    return user ? children : <Navigate to="/login" />;
};
```

## User Registration: Setting up the layout
The registration form collects user details such as name, email, and password, and submits them to the backend for account creation.

## User Registration: Building the Flow
Once the user registers successfully, the backend stores their credentials securely and sends a confirmation response.

## Implementing LogOut Functionality
Logging out clears the user session and redirects them to the login page.

### Example Logout Functionality in React:
```jsx
const handleLogout = () => {
    dispatch(logoutAction());
    navigate("/login");
};
```

## Improving User Experience with Spinners
Adding loading spinners enhances UX when authentication-related requests are processing.

## Redirecting User to Home After Login
Upon successful login, users are redirected to the home page or their dashboard.

### Example Redirect in React:
```jsx
useEffect(() => {
    if (user) navigate("/dashboard");
}, [user]);
```

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)