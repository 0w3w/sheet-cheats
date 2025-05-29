
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

### Implementation in Spring Data JPA

Spring Data JPA lets you define query methods just by naming them according to a convention — no need to write SQL/JPQL for simple queries.

#### ✅ General Format

```
findBy[FieldName][Operation][MoreConditions]OrderBy[Field]Asc|Desc
```

Spring will automatically generate the query based on the method name.


#### 🔑 Common Keywords

| Keyword                                                 | Description             | Example                                 |
| ------------------------------------------------------- | ----------------------- | --------------------------------------- |
| `findBy` / `readBy` / `getBy`                           | Start of query          | `findByUsername`                        |
| `And`, `Or`                                             | Logical operators       | `findByFirstNameAndLastName`            |
| `Is`, `Equals`                                          | Optional equality       | `findByAge`, `findByAgeIs`              |
| `Between`, `LessThan`, `GreaterThan`, `After`, `Before` | Comparison              | `findByCreatedDateAfter`                |
| `Like`, `Containing`, `StartingWith`, `EndingWith`      | String matching         | `findByEmailContaining`                 |
| `In`, `NotIn`                                           | Collections             | `findByStatusIn(List<String> statuses)` |
| `Not`, `IsNot`                                          | Negation                | `findByStatusNot(String status)`        |
| `OrderBy`                                               | Sorting                 | `findByStatusOrderByCreatedDateDesc`    |
| `IgnoreCase`                                            | Case-insensitive search | `findByUsernameIgnoreCase`              |


#### 📘 Examples

```java
// Exact match
List<User> findByUsername(String username);

// Multiple conditions
List<User> findByFirstNameAndLastName(String firstName, String lastName);

// String contains
List<User> findByEmailContaining(String keyword);

// Greater than
List<User> findByAgeGreaterThan(int age);

// Between two dates
List<Order> findByOrderDateBetween(LocalDate start, LocalDate end);

// Collection match
List<User> findByRoleIn(List<String> roles);

// Case-insensitive match
List<User> findByUsernameIgnoreCase(String username);

// Sorted results
List<User> findByActiveTrueOrderByLastLoginDesc();
```

#### ⚠️ Tips

* Field names must match **entity property names** (not database column names).
* Use **camel case** for multi-word fields: `findByLastNameAndFirstName`.
* For complex queries, prefer `@Query` with custom JPQL or native SQL.

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

