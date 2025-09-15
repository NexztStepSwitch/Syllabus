# 📘 System Design (HLD + LLD) — Syllabus

---

## 1. Fundamentals of System Design
- **Definition & Scope**
  - High-Level Design (HLD)
  - Low-Level Design (LLD)
- **System Characteristics**
  - Scalability
  - Availability
  - Reliability
  - Maintainability
  - Performance
- **Key Principles**
  - Separation of concerns
  - Modularity
  - Abstraction
  - Encapsulation
  - Reusability

---

## 2. High-Level Design (HLD)
### 2.1 System Requirements
- Functional requirements
- Non-functional requirements
- Constraints & assumptions

### 2.2 Architectural Styles & Patterns
- **Monolithic Architecture**
- **Layered Architecture**
- **Microservices Architecture**
- **Event-Driven Architecture**
- **Serverless Architecture**
- **Service-Oriented Architecture (SOA)**

### 2.3 Design Components
- API Gateways
- Load Balancers
- Databases (SQL, NoSQL)
- Caches
- Message Queues (Kafka, RabbitMQ)
- Object Storage (S3, GCS, Azure Blob)

### 2.4 Data Management
- Database design (Normalization, Denormalization)
- Sharding, Replication, Partitioning
- Indexing strategies
- Transactions & Concurrency Control (ACID vs BASE)

### 2.5 Scalability & Performance
- Horizontal vs Vertical Scaling
- Consistency, Availability, Partition Tolerance (CAP theorem)
- Latency vs Throughput
- Rate Limiting & Throttling
- Caching Strategies
  - Client-side, CDN, Reverse proxy (Varnish, Nginx), DB caching (Redis, Memcached)

### 2.6 Reliability & Fault Tolerance
- Failover mechanisms
- Replication
- Circuit breaker pattern
- Retry policies
- Disaster recovery (RPO, RTO)

### 2.7 Security Considerations
- Authentication (OAuth2, JWT, SAML)
- Authorization (RBAC, ABAC)
- Encryption (at rest & in transit)
- API security (rate limits, throttling, IP whitelisting)
- DDoS prevention

### 2.8 Observability
- Logging
- Metrics
- Distributed Tracing
- Monitoring & Alerting tools (Prometheus, Grafana, ELK, Jaeger)

---

## 3. Low-Level Design (LLD)
### 3.1 Core Concepts
- Object-Oriented Design Principles
  - SOLID Principles
  - DRY (Don’t Repeat Yourself)
  - KISS (Keep It Simple, Stupid)
  - YAGNI (You Aren’t Gonna Need It)
- UML Diagrams
  - Class Diagram
  - Sequence Diagram
  - Activity Diagram
  - State Diagram

### 3.2 Design Patterns
- **Creational Patterns**
  - Singleton
  - Factory
  - Abstract Factory
  - Builder
  - Prototype
- **Structural Patterns**
  - Adapter
  - Composite
  - Proxy
  - Decorator
  - Facade
- **Behavioral Patterns**
  - Strategy
  - Observer
  - Command
  - Chain of Responsibility
  - Template Method

### 3.3 API Design
- REST Principles
  - Resource modeling
  - Status codes
  - Versioning
  - Pagination
- GraphQL (intro)
- gRPC (intro)

### 3.4 Database Modeling in LLD
- ER Diagrams
- Relationships (1:1, 1:N, M:N)
- Schema design examples (e.g., e-commerce, banking)
- Optimizations (indexes, foreign keys)

### 3.5 Concurrency in LLD
- Thread safety
- Synchronization
- Locks
- Optimistic vs Pessimistic concurrency
- Event loops

### 3.6 Error Handling & Logging
- Exception design
- Structured logging
- Correlation IDs

---

## 4. Practice & Case Studies
- Design **URL Shortener** (e.g., TinyURL)
- Design **Uber/Lyft** (Ride-hailing system)
- Design **Instagram/WhatsApp**
- Design **E-commerce System**
- Design **Distributed File Storage** (Google Drive, Dropbox)
- Design **Payment Gateway**
- Design **Rate Limiter**

---

## 5. Interview-Oriented Checklist
- Be able to explain **trade-offs** between designs
- Communicate **assumptions** clearly
- Use diagrams (HLD → block diagrams, LLD → UML)
- Optimize for scalability, fault-tolerance, and maintainability
