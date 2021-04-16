# Introduction to Maven and JUnit

---

## What is Maven?

Maven is a tool that provides a reliable mechanism to standardize the build process. It has build phases that you can attach different plugins, and a repository for your jars and libraries.

---

## Why Maven?

From the Maven documentation, its goals are:

- Making the build process easy
- Providing a uniform build system
- Providing quality project information
- Providing guidelines for best practices development
- Allowing transparent migration to new features

---

## Benefits of Maven

- Most teams prefer to have a standardized build system for handling projects
- It is free
- It is used by most of Java developers
- It is backed by Apache.

---

## The Project Object Model (XML)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.launchacademy</groupId>
  <artifactId>jansiExample</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

---

## What is XML?

- Thus far, we've used **json** as a serialization format
- Generally, we can use `json` or `xml` to represent data
- Java really likes XML
- `json` is more concise, `xml` is more structured

---

## Benefits of XML

- Just like HTML, XML can represent hierarchies of data
- We can contextualize data with XML attributes
- XML can be validated against a schema to ensure it's well-formed

---

## Maven and IntelliJ: Creating a Project

1. Create a Maven Project by using the `Create New Project`.
2. On the next dialogue box, select `Maven` from the list on the left. Click the `next` button.
3. Give your project a groupId (`com.launchacademy`)
4. Provide an artifactId (usually the project name)
5. Keep the SNAPSHOT version the same.
6. Click the `Next` button and click `Next` button on the next page as well.

---

## Enable Auto-Import

A dialog will pop up on the lower right hand side, click on `"Enable Auto-Import"`. This will tell IntelliJ to automatically import all dependencies into your `.m2` directory and add it to your project.

---

## Maven and IntelliJ: Adding to an existing project

To convert a Java project into a Maven project:

1. Right click (or control-click) on the `module` name
2. Select `"Add Framework Support..."`
3. In the resulting left column, click on the `Maven` box and click on the `Ok` button

This will create a Maven project though you will have to fill out the groupId in the `pom.xml` file.

---

## Standard Directories for Maven

- `src/main/java` is for your Java source files.
- `src/main/resources` is for your properties and other resource files (images, data files, etc)
- `src/test/java` is where you place your java and JUnit test files.
- `src/test/resources` is for your test properties and other resource files.

---

## Defining Dependencies

Use the `dependencies` and `dependency` tags to set up all your jars and other dependencies.

```xml
<dependencies>
   <dependency>
     <groupId>org.hibernate</groupId>
     <artifactId>hibernate-core</artifactId>
     <version>5.4.2.Final</version>
   </dependency>
   ...
</dependencies>
```

---

## But where does it store the jars?

Everything is placed and organized for you in `~/.m2`

---

## Where can I find dependencies to use?

- The Maven Registry ([mvnregistry.com](mvnregistry.com))
- GitHub

Look for:

- Popularity
- Commit / Update activity
- Tests!

---

## JUnit

---

## JUnit Defined

JUnit is a test harness that is the favorite of Java developers. We will be using JUnit 5 which is latest version

We'll use it to practice TDD in Java

---

## Setting up JUnit - Adding Some Properties

```xml
<properties>
  <java.version>11</java.version>
  <maven.compiler.source>${java.version}</maven.compiler.source>
  <maven.compiler.target>${java.version}</maven.compiler.target>
  <junit.jupiter.version>5.4.2</junit.jupiter.version>
</properties>
```

Placing these here keeps your `pom.xml` DRY

---

## Setting up JUnit - Add the Dependency

Add the dependencies to `pom.xml`

```xml
<dependency>
   <groupId>org.junit.jupiter</groupId>
   <artifactId>junit-jupiter-api</artifactId>
   <version>${junit-platform.version}</version>
   <scope>test</scope>
 </dependency>
 <dependency>
   <groupId>org.junit.jupiter</groupId>
   <artifactId>junit-jupiter-engine</artifactId>
   <version>${junit-platform.version}</version>
   <scope>test</scope>
 </dependency>
```

---

## Setting up JUnit - Add the Plugin

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>2.22.0</version>
  <configuration>
    <argLine>--illegal-access=permit</argLine>
  </configuration>
</plugin>
```

Remember, Maven is a packaging platform. We will eventually want to integrate our tests into the packaging process.

---

## Setting Up Your First Test

Create a Plain Old Java Object (POJO) in the test directory. All you need is to use the `@Test` annotation on your testing method.

```java
public class ExampleTest {
  @Test
  public void addingTest() {
    ...
  }
}
```

---

## Wait, What's an Annotation?

- Initially, annotations were used exclusively to document code
- Over time, they've become more functional
- JUnit extensively uses annotations

---

## Assertions

```Java
assertEquals(5*3, calc.multiply(5,3));
```

---

### Before and After

`@BeforeAll` and `@AfterAll` annotations run code before and after the entire test suite.

```Java
@BeforeAll
void init() {
  Scanner inScanner = new Scanner(System.in);
}

@AfterAll
void teardown() {
  inScanner.close();
}
```

---

## Maven Unit test directory

Since Maven has its standard directory, you place your java unit tests in the `test/java` directory. Maven will automatically run them.

---

## IntelliJ and JUnit

- Click on a class definition and ALT-Enter or OPT-Enter to see the "intention actions".
- To run it, you can either add it to your menu, click on the double triangles by the main class of your test, or run it from Maven.
