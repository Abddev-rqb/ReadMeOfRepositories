# Introduction to Annotations in Spring Framework

Annotations in the Spring Framework simplify configuration and dependency injection, reducing the need for XML-based configurations. They enhance modularity and ease maintenance by providing metadata at the class level.

## Understanding Components and `@ComponentScan`

- `@Component`: Marks a Java class as a Spring-managed component.
- `@ComponentScan`: Instructs Spring to scan the specified package for components, services, and repositories.

### Example:

```java
import org.springframework.stereotype.Component;

@Component  // Marks this class as a Spring-managed component
public class MyComponent {
    public void display() {
        System.out.println("Hello from MyComponent!");
    }
}
```

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("com.example")  // Scans the package for Spring components
public class AppConfig {
}
```

---

## Hands-on: Component and Component Scan with Spring (Without Annotations)

Before annotations, Spring beans were defined in XML:

### `beans.xml`:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myComponent" class="com.example.MyComponent"/>
</beans>
```

### Java Code:

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        MyComponent myComponent = context.getBean(MyComponent.class);
        myComponent.display();
    }
}
```

---

## `@Value` Annotation

`@Value` is used to inject values into fields from property files or hardcoded values.

### Example:

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class AppConfig {
    @Value("${app.name}")
    private String appName;

    public void showAppName() {
        System.out.println("Application Name: " + appName);
    }
}
```

### `application.properties`:

```
app.name=Spring Annotation Demo
```

---

## Transition from XML to Annotations in Spring Framework

With XML:

```xml
<bean id="myService" class="com.example.MyService"/>
```

With Annotations:

```java
import org.springframework.stereotype.Service;

@Service
public class MyService {
}
```

No need to define the bean in XML when using `@Service`.

---

## `@Autowired` Annotation

`@Autowired` is used for dependency injection in Spring.

### Example:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class UserService {
    @Autowired
    private MyComponent myComponent;

    public void process() {
        myComponent.display();
    }
}
```

---

## `@Qualifier` Annotation

`@Qualifier` is used to specify which bean to inject when multiple beans of the same type exist.

### Example:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class PaymentService {
    @Autowired
    @Qualifier("creditCardPayment")
    private PaymentProcessor paymentProcessor;
}
```

---

## Pagination in README.md (Table of Contents)

### Table of Contents

- [Introduction to Annotations](#introduction-to-annotations-in-spring-framework)
- [Understanding Components and `@ComponentScan`](#understanding-components-and-componentscan)
- [Hands-on: Component and Component Scan without Annotations](#hands-on-component-and-component-scan-with-spring-without-annotations)
- [`@Value` Annotation](#value-annotation)
- [Transition from XML to Annotations](#transition-from-xml-to-annotations-in-spring-framework)
- [`@Autowired` Annotation](#autowired-annotation)
- [`@Qualifier` Annotation](#qualifier-annotation)


