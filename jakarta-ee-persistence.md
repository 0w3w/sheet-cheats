# 🌐 Jakarta EE Persistence (JPA) Cheat Sheet

## 🔧 Basic Annotations

| Annotation | Description |
|-----------|-------------|
| `@Entity` | Marks a class as a JPA entity |
| `@Table(name="table_name")` | Maps entity to a specific table |
| `@Id` | Denotes primary key |
| `@GeneratedValue` | Strategy for primary key generation |
| `@Column(name="column_name")` | Maps a field to a DB column |
| `@Transient` | Field is not persisted |
| `@Lob` | Marks a field for large object (BLOB/CLOB) |

## 🔑 Primary Key Generation Strategies

```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
@GeneratedValue(strategy = GenerationType.SEQUENCE)
@GeneratedValue(strategy = GenerationType.TABLE)
@GeneratedValue(strategy = GenerationType.AUTO)
```

## 📚 Relationships

| Annotation | Description |
|-----------|-------------|
| `@OneToOne` | 1:1 relationship |
| `@OneToMany` | 1:N relationship |
| `@ManyToOne` | N:1 relationship |
| `@ManyToMany` | N:N relationship |
| `@JoinColumn(name="...")` | Foreign key column |
| `@JoinTable(...)` | Join table for many-to-many |

## 🔄 Cascade Types

```java
CascadeType.PERSIST
CascadeType.MERGE
CascadeType.REMOVE
CascadeType.REFRESH
CascadeType.DETACH
CascadeType.ALL
```

Usage:
```java
@OneToMany(cascade = CascadeType.ALL)
```

## 📦 Entity Lifecycle Callbacks

| Annotation | Trigger |
|------------|---------|
| `@PrePersist` | Before insert |
| `@PostPersist` | After insert |
| `@PreUpdate` | Before update |
| `@PostUpdate` | After update |
| `@PreRemove` | Before delete |
| `@PostRemove` | After delete |
| `@PostLoad` | After entity load |

## 📥 Basic Queries (JPQL)

```java
SELECT e FROM Entity e
SELECT e FROM Entity e WHERE e.name = :name
```

Use with:
```java
@PersistenceContext
EntityManager em;

List<User> users = em.createQuery("SELECT u FROM User u", User.class)
                     .getResultList();
```

## ✍️ CRUD via `EntityManager`

```java
em.persist(entity);              // Create
em.find(Entity.class, id);       // Read
em.merge(entity);                // Update
em.remove(entity);               // Delete
```

## ⚙️ Configuration (`persistence.xml`)

```xml
<persistence xmlns="https://jakarta.ee/xml/ns/persistence"
             version="3.0">
  <persistence-unit name="myPU">
    <class>com.example.MyEntity</class>
    <properties>
      <property name="jakarta.persistence.jdbc.url" value="jdbc:h2:mem:test"/>
      <property name="jakarta.persistence.jdbc.driver" value="org.h2.Driver"/>
      <property name="jakarta.persistence.jdbc.user" value="sa"/>
      <property name="jakarta.persistence.jdbc.password" value=""/>
      <property name="jakarta.persistence.schema-generation.database.action" value="create"/>
    </properties>
  </persistence-unit>
</persistence>
```
