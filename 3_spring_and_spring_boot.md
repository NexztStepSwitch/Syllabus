# 🌱 Spring & Spring Boot – Detailed Syllabus

### ⭐ Importance: ★★★★★ (5/5)

---

## 1. **Spring Core**
- **IoC (Inversion of Control)**
  - Dependency Injection (Constructor, Setter, Field)
  - Bean lifecycle
  - ApplicationContext vs BeanFactory
- **Beans**
  - Bean scopes (singleton, prototype, request, session)
  - Bean initialization & destruction methods
  - Autowiring modes
- **Configuration**
  - XML-based configuration
  - Annotation-based configuration (`@Component`, `@Configuration`, `@Bean`, `@Autowired`, `@Qualifier`)
  - Java-based configuration

---

## 2. **Spring AOP (Aspect-Oriented Programming)**
- **Concepts**
  - Aspect, Join Point, Advice, Pointcut, Weaving
- **Types of advice**
  - Before, After, Around, AfterReturning, AfterThrowing
- **Use cases**
  - Logging
  - Transaction management
  - Security
- **Implementation**
  - `@Aspect`, `@EnableAspectJAutoProxy`

---

## 3. **Spring Data Access**
- **Spring JDBC**
  - JdbcTemplate
  - NamedParameterJdbcTemplate
  - Exception translation
- **ORM Integration**
  - Hibernate with Spring
  - JPA (Java Persistence API)
  - EntityManager
- **Transactions**
  - Programmatic vs Declarative
  - `@Transactional`
  - Propagation & Isolation levels
  - Rollback rules

---

## 4. **Spring MVC**
- **DispatcherServlet architecture**
- **Controllers**
  - `@Controller` vs `@RestController`
  - Request mapping (`@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.)
- **Request handling**
  - Path variables, Request params
  - RequestBody & ResponseBody
  - Data binding & validation (`@Valid`, `@InitBinder`)
- **Views**
  - ViewResolvers
  - JSP, Thymeleaf, FreeMarker

---

## 5. **Spring Boot Fundamentals**
- **Introduction**
  - What is Spring Boot? (convention over configuration)
  - Starter dependencies
  - Auto-configuration
- **Spring Boot Project Structure**
  - `application.properties` vs `application.yml`
  - Profiles (`@Profile`)
  - Configuration properties (`@ConfigurationProperties`)
- **Spring Boot Annotations**
  - `@SpringBootApplication`
  - `@EnableAutoConfiguration`
  - `@ComponentScan`
- **CommandLineRunner & ApplicationRunner**

---

## 6. **Spring Boot Web Development**
- **REST APIs**
  - Building RESTful controllers
  - Request/Response handling
  - Content negotiation (JSON/XML)
  - Versioning APIs
- **Exception Handling**
  - `@ControllerAdvice`
  - `@ExceptionHandler`
  - Custom error response
- **Filters & Interceptors**
  - Use cases: logging, authentication, request modification

---

## 7. **Spring Boot Data & Persistence**
- **Spring Data JPA**
  - Repositories (`CrudRepository`, `JpaRepository`, `PagingAndSortingRepository`)
  - Query methods (derived queries, JPQL, Native queries)
  - Pagination & Sorting
  - Projections
- **Database Configurations**
  - H2, MySQL, PostgreSQL, MongoDB
  - Connection Pooling (HikariCP)
- **Spring Data MongoDB**
  - Document mapping
  - Repositories for NoSQL

---

## 8. **Spring Boot Security**
- **Spring Security Basics**
  - Authentication vs Authorization
  - UserDetails & GrantedAuthority
- **Configuring Security**
  - In-memory authentication
  - JDBC-based authentication
  - Custom UserDetailsService
- **Password Handling**
  - PasswordEncoder (BCrypt, PBKDF2, SCrypt)
- **JWT (JSON Web Token)**
  - Token generation
  - Token validation
  - Stateless authentication
- **OAuth2 & OpenID Connect**
  - Social logins (Google, GitHub)
  - Resource server & authorization server

---

## 9. **Spring Boot Microservices**
- **Microservices architecture**
  - Advantages & challenges
  - Communication styles (REST, Messaging, gRPC)
- **Service Discovery**
  - Netflix Eureka
  - Spring Cloud Consul
- **API Gateway**
  - Netflix Zuul
  - Spring Cloud Gateway
- **Centralized Configuration**
  - Spring Cloud Config Server
- **Circuit Breakers & Resilience**
  - Resilience4j
  - Retry & Fallback
- **Distributed Tracing**
  - Sleuth
  - Zipkin

---

## 10. **Spring Boot Messaging**
- **Message Queues**
  - Kafka
  - RabbitMQ
  - ActiveMQ
- **Spring Cloud Stream**
  - Producers & Consumers
  - Message channels & bindings

---

## 11. **Spring Boot Testing**
- **Unit Testing**
  - JUnit 5
  - Mockito
- **Integration Testing**
  - `@SpringBootTest`
  - MockMvc
- **Testcontainers for DB testing**
- **WireMock for external service mocking**

---

## 12. **Spring Boot Actuator & Monitoring**
- **Actuator Endpoints**
  - Health, Metrics, Info, Beans
- **Custom Actuator Endpoints**
- **Integration with Monitoring Tools**
  - Prometheus
  - Grafana
  - Micrometer

---

## 13. **Spring Boot Deployment**
- **Packaging**
  - JAR vs WAR
  - Embedded Tomcat/Jetty
- **Profiles & Config**
  - Dev, Test, Prod environments
  - Externalized configuration
- **Deployment Environments**
  - Dockerization
  - Kubernetes (K8s)
  - Cloud platforms (AWS, Azure, GCP)

---

## 14. **Spring Boot Best Practices**
- Proper Layered Architecture (Controller → Service → Repository)
- DTOs vs Entities
- Avoiding N+1 queries
- Exception handling consistency
- Logging best practices
- Properties management (`application.yml`, `application.properties`)
