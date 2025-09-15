# 📘 Microservices & Distributed Systems — Syllabus

---

## 1. Fundamentals of Microservices
- **Definition**
  - Difference from monolithic architecture
  - Key characteristics (independent deployability, scalability, autonomy)
- **Benefits**
  - Modularity
  - Independent scaling
  - Fault isolation
  - Technology heterogeneity
- **Challenges**
  - Complexity in communication
  - Data consistency
  - Deployment overhead

---

## 2. Service Design
- Service boundaries
- Domain-Driven Design (DDD)
  - Entities, Value Objects, Aggregates
  - Bounded Contexts
- Service granularity (fine-grained vs coarse-grained)
- API-first design

---

## 3. Communication in Microservices
- **Synchronous**
  - REST
  - gRPC
- **Asynchronous**
  - Message Brokers (Kafka, RabbitMQ, ActiveMQ)
  - Event-driven communication
- **Patterns**
  - Request-Response
  - Publish-Subscribe
  - Event Sourcing
  - CQRS (Command Query Responsibility Segregation)

---

## 4. Distributed Systems Fundamentals
- Characteristics
  - Concurrency
  - No global clock
  - Independent failures
- Key Theorems & Concepts
  - CAP Theorem
  - PACELC Theorem
  - Brewer’s Theorem
- Data Consistency
  - Strong, Eventual, Causal
  - Consensus algorithms (Raft, Paxos, ZAB)

---

## 5. Scalability & Reliability
- **Scaling Approaches**
  - Horizontal vs Vertical scaling
  - Load balancing (Round robin, Least connections, Hashing)
- **Fault Tolerance**
  - Retry patterns
  - Circuit breakers
  - Failover strategies
- **Redundancy**
  - Replication
  - Leader-election
  - Quorum-based writes & reads

---

## 6. Microservices Infrastructure
- Service Discovery (Eureka, Consul, etcd, Zookeeper)
- API Gateway (Kong, Zuul, Nginx, Ambassador)
- Sidecar pattern (Service Mesh — Istio, Linkerd)
- Configuration Management (Spring Cloud Config, Consul)

---

## 7. Security in Microservices
- Authentication
  - OAuth 2.0
  - OpenID Connect
  - JWT
- Authorization
  - Role-based (RBAC)
  - Attribute-based (ABAC)
- Network security
  - mTLS between services
  - API Gateway rate-limiting
- Secret Management (Vault, AWS KMS)

---

## 8. Data Management
- Database per service pattern
- Event sourcing
- Saga pattern (choreography, orchestration)
- Outbox pattern
- Two-phase commit vs eventual consistency

---

## 9. Observability in Microservices
- Centralized Logging (ELK, EFK)
- Distributed Tracing (Jaeger, Zipkin)
- Metrics (Prometheus, Grafana)
- Health checks (liveness, readiness)

---

## 10. Case Studies & Hands-on Practice
- Design & implement a **URL shortener** with microservices
- Build an **e-commerce checkout system**
- Implement **user authentication & authorization** service
- Event-driven **order management system**

---

## 11. Interview Preparation Checklist
- Explain trade-offs between monoliths & microservices
- Design patterns for distributed systems
- Handling failures gracefully
- Scaling services efficiently
- Ensuring data consistency across services
