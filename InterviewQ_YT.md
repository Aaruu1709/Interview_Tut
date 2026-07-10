
---

# Round 1 – Technical + Project Discussion

### 1. Tell me about yourself.

---

### 2. Explain your current project.

(Follow-up questions were asked based on the project.)

---

### 3. You have been working on this project for over a year.

**Tell me, was there ever a situation where something worked perfectly on your local machine but completely broke in production?**

---

### 4. Your team has a shared `HashMap` inside a Singleton Bean that stores temporary user session data.

After a load test, users started seeing each other's data.

**What went wrong? Explain it to your team.**

---

### 5. In Spring Boot,

If one `@Transactional` method calls another `@Transactional` method **within the same class**, do you think the transaction will behave the way you expect?

**Have you ever faced this situation?**

---

### 6. How do you make sure your APIs don't break existing clients when your team releases a new version?

Walk me through your approach.

Assume you **cannot force all clients to upgrade immediately.**

---

### 7. Imagine you have three microservices.

* Order Service
* Payment Service
* Notification Service

A user places an order.

The system has to

* Deduct inventory
* Charge the customer
* Send a confirmation email

Now suppose

* Payment succeeds
* Inventory is deducted
* Email notification fails

**How would you handle this situation?**

---

### 8. Suppose you deploy your service on Friday evening.

By Saturday morning your on-call team reports HTTP 500 errors.

Your own service looks fine, but a downstream service is flaky.

By Saturday afternoon your thread pool is completely exhausted and your own service crashes.

**Why did this happen?**

**What should have been implemented to prevent it?**

---

# Round 2 – Coding

### 9. Given a list of strings,

without using any built-in sorting method,

find the **top two most frequently occurring words.**

---

### Follow-up

Handle edge cases like

* Empty list
* Duplicate frequencies
* All words having the same frequency

---

### 10. Using Java 8 Streams,

you have a list of Transaction objects.

Each object contains

* amount
* date
* category

Find the **total transaction amount per category**

but only for transactions that happened in the **last 30 days.**

---

### 11. You have 12 microservices.

Each has its own database.

Service A needs data that exists inside Service B's database.

**How will Service A get that data without directly accessing Service B's database?**

---

### 12. What are the advantages of Microservices?

---

### 13. Monolithic vs Microservices.

---

### 14. Explain basic Microservice Design Patterns.

---

### 15. Explain Circuit Breaker Pattern.

---

### 16. Explain Resilience Pattern.

---

# HR Round

### 17. You have spent more than three years in your current company.

**What is your current company not giving you that you are hoping to find here?**

---

### 18. Tell me about a time when something you built went wrong in production.

What happened?

What did you do?

---

### 19. How do you feel about working with global clients?

We have teams in the UK and Singapore.

---

### 20. What are your salary expectations?

---

# ⭐ Hidden Concepts the Interviewer Expected

The interviewer never directly asked these terms but expected the candidate to identify them:

* Production Debugging
* Environment Configuration
* Thread Safety
* Singleton Bean
* HashMap vs ConcurrentHashMap
* `@Transactional`
* Spring AOP Proxy
* API Versioning
* Backward Compatibility
* Saga Pattern
* Compensation Transaction
* Choreography
* Orchestration
* Kafka
* Circuit Breaker
* Resilience4j
* Retry
* Timeout
* Fallback
* Thread Pool Exhaustion
* Cascading Failure
* Java 8 Streams
* `Collectors.groupingBy()`
* `Collectors.summingDouble()`
* REST Communication
* gRPC
* Event-Driven Architecture
* Eventual Consistency

---

This interview contains around **20 direct questions**, but behind them it tests nearly **30–35 important backend concepts**. Since you're targeting a **4+ years Java Backend Developer** role, we can prepare every one of these with interview-ready answers and production examples.
