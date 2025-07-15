
---

# 📚 Spring Framework Interview Guide

A comprehensive, clear, and detailed guide to frequently asked Spring Framework interview questions — suitable for backend engineers preparing for interviews or as a technical reference.

---

## 📌 Core Concepts

### What is Loose Coupling?

Loose coupling means reducing dependencies between components in a system, so changes in one component have minimal impact on others. In Spring, this is achieved using interfaces, dependency injection, and inversion of control (IoC).

**Example:**
A `PaymentService` depending on a `PaymentGateway` interface rather than a specific implementation like `StripePaymentGateway`.

---

### What is a Dependency?

A dependency is any object that a class requires to function. For instance, a `UserService` might require a `UserRepository` to access the database — making the repository a dependency.

---

### What is IoC (Inversion of Control)?

IoC is a principle where the control of object creation, configuration, and management is shifted from the application code to a container or framework (like Spring).
Instead of creating dependencies manually, you declare them and let the IoC container provide them at runtime.

---

### What is Dependency Injection?

Dependency Injection (DI) is a design pattern implementing IoC. It allows an external entity (the Spring container) to inject dependencies into a class.

**Types of Dependency Injection:**

* **Constructor Injection**
* **Setter Injection**
* **Field Injection (via `@Autowired`)**

---

## 📦 Dependency Injection & Autowiring

### Can you give a few examples of Dependency Injection?

* **Constructor Injection:**

  ```java
  @Component
  public class OrderService {
      private final PaymentService paymentService;

      @Autowired
      public OrderService(PaymentService paymentService) {
          this.paymentService = paymentService;
      }
  }
  ```

* **Setter Injection:**

  ```java
  @Component
  public class OrderService {
      private PaymentService paymentService;

      @Autowired
      public void setPaymentService(PaymentService paymentService) {
          this.paymentService = paymentService;
      }
  }
  ```

---

### What is Autowiring?

Autowiring allows Spring to automatically inject the required dependencies without explicitly specifying them in configuration files or constructors.

---

### Important roles of an IoC Container:

* Instantiates beans.
* Configures bean dependencies.
* Manages bean life cycles.
* Provides services like AOP, event propagation, and resource management.
* Manages scopes and proxies.

---

## 🏗️ BeanFactory vs ApplicationContext

### What are BeanFactory and ApplicationContext?

* **BeanFactory:** Basic IoC container, lazily initializes beans.
* **ApplicationContext:** Enhanced container extending `BeanFactory`, eagerly loads beans and provides additional enterprise features like event publishing, AOP integration, and internationalization.

---

### Comparison:

| Feature             | BeanFactory | ApplicationContext    |
| :------------------ | :---------- | :-------------------- |
| Lazy Initialization | Yes         | No (eager by default) |
| AOP Support         | No          | Yes                   |
| Event Handling      | No          | Yes                   |
| Message Source      | No          | Yes                   |

---

## 📍 Component Scanning

### How does Spring know where to search for Components or Beans?

Through **component scanning**, configured via annotations (`@ComponentScan`) or XML.

---

### What is a Component Scan?

A process by which Spring automatically detects and registers beans annotated with `@Component`, `@Service`, `@Repository`, or `@Controller` within specified packages.

---

### How do you define a Component Scan?

* **XML Configuration:**

  ```xml
  <context:component-scan base-package="com.example.app"/>
  ```

* **Java Configuration:**

  ```java
  @Configuration
  @ComponentScan("com.example.app")
  public class AppConfig {}
  ```

* **Spring Boot:**
  Automatically scans from the package of the main class annotated with `@SpringBootApplication`.

---

## 🏷️ Spring Annotations

### What does `@Component` signify?

Marks a Java class as a Spring-managed bean.

---

### What does `@Autowired` signify?

Marks a constructor, field, or setter method for dependency injection by Spring’s IoC container.

---

### Difference Between `@Component`, `@Service`, `@Repository`, `@Controller`

* `@Component`: Generic stereotype for any Spring-managed component.
* `@Service`: Indicates a service-layer class containing business logic.
* `@Repository`: Indicates a data-access-layer class and enables exception translation.
* `@Controller`: Indicates a web controller handling HTTP requests.

---

## 📝 Bean Scope & Thread Safety

### What is the default scope of a bean?

**Singleton** — one instance per Spring IoC container.

---

### Are Spring beans thread-safe?

**No.** Singleton beans are not thread-safe by default unless explicitly synchronized.

---

### Other Scopes Available:

* `prototype`
* `request` (web apps)
* `session` (web apps)
* `application` (web apps)
* `websocket`

---

### How is Spring’s singleton bean different from GoF Singleton Pattern?

* **GoF Singleton:** One instance per JVM.
* **Spring Singleton:** One instance per IoC container.

---

## 📚 Dependency Injection Types

### Different types:

* Constructor Injection
* Setter Injection
* Field Injection (via `@Autowired`)

---

### What is Setter Injection?

Dependencies injected via public setter methods.

---

### What is Constructor Injection?

Dependencies provided through class constructors.

---

### How do you choose between Setter and Constructor Injections?

* Use **Constructor Injection** for required dependencies.
* Use **Setter Injection** for optional or mutable dependencies.

---

## 📂 Application Context Creation

### Different options:

* `ClassPathXmlApplicationContext`
* `AnnotationConfigApplicationContext`
* `WebApplicationContext`

---

### XML vs. Java Configuration

* **XML:** Externalized, declarative, older.
* **Java Config:** Type-safe, annotation-driven, modern.

**Prefer Java Configuration in modern applications.**

---

## ⚙️ Autowiring Mechanics

### How does Spring do Autowiring?

By matching beans:

* By Type
* By Name
* Using `@Qualifier`
* Using `@Primary`

---

### Debugging Autowiring Problems

* Check component scan paths.
* Use `@Qualifier` to resolve conflicts.
* Mark default beans with `@Primary`.

---

### How to solve NoUniqueBeanDefinitionException?

* Use `@Qualifier` to specify the desired bean.
* Or mark one bean as `@Primary`.

---

### How to solve NoSuchBeanDefinitionException?

* Ensure correct component scanning.
* Check bean names and configurations.
* Confirm the dependency type exists.

---

## 🎛️ Advanced Annotations

### What is `@Primary`?

Indicates a bean should be the primary candidate when multiple beans of the same type exist.

### What is `@Qualifier`?

Used to specify which exact bean should be injected when multiple candidates are present.

---

## 📑 CDI vs Spring DI

### What is CDI?

A Java EE standard for dependency injection (Contexts and Dependency Injection).

### Does Spring support CDI?

Yes, but Spring has its own DI mechanism.

### Would you recommend CDI or Spring Annotations?

For Spring applications, **use Spring annotations**. They are better integrated with the framework.

---

## 🔄 Version Features

### New Features in Spring 4.0

* Java 8 support.
* WebSocket support.
* Groovy bean DSL.

### New Features in Spring 5.0

* Reactive Programming (Spring WebFlux).
* Java 8+ baseline.
* Functional bean registration.

---

## 🌿 Spring Ecosystem

### Important Spring Modules

* Core Container (Core, Beans, Context, Expression Language)
* Spring AOP
* Spring JDBC
* Spring ORM
* Spring Web MVC
* Spring Security
* Spring Test

---

### Important Spring Projects

* Spring Boot
* Spring Cloud
* Spring Data
* Spring Security
* Spring Batch
* Spring Integration

---

## 📦 Dependency Management

### Simplest Way to Ensure Single Version of All Dependencies:

Use **Spring Boot’s Dependency Management via BOM (Bill of Materials)**.

---

## 📐 Design Patterns Used in Spring

* Singleton
* Factory
* Proxy
* Template Method
* Dependency Injection
* MVC

---

## 📣 Final Thoughts

### What do you think about Spring Framework?

It’s a robust, modular, and versatile framework that simplifies enterprise Java application development by providing powerful infrastructure support.

### Why is Spring Popular?

* Loose coupling via DI.
* Rich ecosystem.
* Powerful abstractions.
* Active community.
* Microservices-friendly with Spring Boot.

### Big Picture of the Spring Framework:

A comprehensive platform covering:

* **Core:** IoC, DI, AOP.
* **Web:** MVC, REST.
* **Data:** JDBC, JPA.
* **Security:** Authentication/Authorization.
* **Reactive:** WebFlux.
* **Cloud:** Spring Boot & Spring Cloud.

---
