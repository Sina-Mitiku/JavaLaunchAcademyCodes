# Working with Hibernate

---

## Object Relational Mapping (ORM)

- Bridges the gap between our database tables and Java objects
- Can handle saving, retrieving, deleting, and relating our objects together

---

## Hibernate Sessions and the JPA

- When working with the JPA, we use an `EntityManager` in conjunction with annotated classes
- We also use POJOs called Beans (Java Beans... get it?)
- These are very simple Java objects that help us interface between our code and the database
- Instead of using a constructor to instantiate the object we use the annotated class's (aka entity) setters.

---

## Configuration

```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="2.2"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd">
  <!-- Define persistence unit -->
  <persistence-unit name="com.launchacademy.quotes">
    <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
    <properties>
      <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://localhost:5432/quotes" />
      <property name="javax.persistence.jdbc.driver" value="org.postgresql.Driver" />
      <property name="javax.persistence.jdbc.user" value="postgres" />
      <property name="javax.persistence.jdbc.password" value="password" />
    </properties>
  </persistence-unit>
</persistence>
```

---

## The EM and EMF

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;
public class Main {
  public static void main(String[] args) {
    EntityManagerFactory emf =
    Persistence.createEntityManagerFactory("com.launchacademy.quotes");
    EntityManager em = emf.createEntityManager();
    try {
      // our database interactions can go here
    }
    finally {
      em.close();
      emf.close();
    }
  }
}
```

---

```java

try {
  Quote quotes = new Quote();
  quotes.setQuote("Clever Girl");
  quotes.setAuthor("Muldoon");
  quotes.setSubject("Raptors")

  Author author = new Author();
  author.setFirstName("Michael")
  author.setLastName("Creighton")
  em.getTransaction().begin();
  em.persist(quotes);
  em.persist(author)
  em.getTransaction().commit();
}
finally {
  em.close();
  emf.close();
}


```

---

## Wait - What's a Bean?

- A Java Bean is a special kind of POJO (Java class)
- It must have a zero argument constructor for easy creation
- It must have getters and setters defined for all of its fields
- Officially it must also implement the `Serializable` interface (don't worry about that for now)

---

## What does an annotated class look like?

```java
@Entity
@Table(name = "quotes")
public class Quote {
  @Id
  @SequenceGenerator(name="quotes_generator", sequenceName="quotes_id_seq",
   allocationSize = 1)
  @GeneratedValue(strategy=GenerationType.SEQUENCE,
   generator="quotes_generator")
  @Column(name="id", nullable=false, unique=true)
  private Long id;

  @Column(name="quote", nullable = false, length = 3000)
  private String name;

  @Column(name="author", nullable = false)
  private String author;

  @Column(name="subject", nullable = false)
  private String subject;

  public Long getId() {
    return id;
  }
  public void setId(Long id) {
    this.id = id;
  }
  public String getName() {
    return weight;
  }
  public void setName(String name) {
    this.name = name;
  }
  public String getAuthor() {
    return weight;
  }
  public void setAuthor(String author) {
    this.name = name;
  }
  public String getSubject() {
    return weight;
  }
  public void setSubject(String subject) {
    this.name = name;
  }


}
```

---

## @Entity

- This marks the class as a JPA entity object
- An "entity" is a _mapped class_

---

## @Table

- Tells Hibernate which table this class maps to
- We need to hand the "argument" of the table name
- Our schema has to create this table

---

## @Id

- Marks the column as a primary key
- We will typically call the column `id`, but don't have to

---

## @SequenceGenerator and @GeneratedValue

- `@SequenceGenerator` ties our `@Id` field to our database sequence
- The JPA has a strategy for incrementing the primary key. We specify our choice with `@GeneratedValue`. It can be:
  - `IDENTITY` increment for an identity column
  - `SEQUENCE` increment for the database sequence
  - `TABLE` increment using the underlying database table
- Our choice largely depends on the type of database we're using!

---

## @Column

- Marks that this field maps to a column in the database
- We tell it the name of the column
- We can also hand it validations such as `nullable`, `unique`, and `length`
