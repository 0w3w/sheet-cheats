
# Spring Framework Stereotypes Cheat Sheet

Spring Framework provides several annotations that act as **stereotypes** to indicate the role of a class in a Spring application.

---

## @Component
- **Description**: Generic stereotype for any Spring-managed component.
- **Use Case**: The most general stereotype, indicating a class is a Spring-managed component, eligible for automatic detection and bean creation.
- **Example**:
  ```java
  @Component
  public class MyComponent {
      // ...
  }
  ```

---

## @Repository
- **Description**: Specialization of `@Component` for persistence layer.
- **Use Case**: Marks a class as a data access component, typically interacting with databases or other data stores, and often used with DAOs (Data Access Objects).
- **Benefits**: Enables exception translation into Spring’s DataAccessException.
- **Example**:
  ```java
  @Repository
  public class MyRepository {
      // ...
  }
  ```

---

## @Service
- **Description**: Specialization of `@Component` for service layer.
- **Use Case**: Specifies a class that handles business logic, often acting as an intermediary between controllers and repositories.
- **Example**:
  ```java
  @Service
  public class MyService {
      // ...
  }
  ```

---

## @Controller
- **Description**: Specialization of `@Component` for presentation layer.
- **Use Case**: Used in Spring MVC to handle HTTP requests.
- **Example**:
  ```java
  @Controller
  public class MyController {
      // ...
  }
  ```

---

## @RestController
- **Description**: Combination of `@Controller` and `@ResponseBody`.
- **Use Case**: Used for RESTful web services.
- **Example**:
  ```java
  @RestController
  public class MyRestController {
      // ...
  }
  ```

---

## Key Notes
- All stereotype annotations are detected through classpath scanning using `@ComponentScan`.
- These annotations help in organizing your application into layers.

