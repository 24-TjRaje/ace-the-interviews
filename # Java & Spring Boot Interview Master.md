# Java & Spring Boot Interview Master Repository

**Target Experience:** 5–8 Years  
**Target Companies:** Service-Based MNCs  
**Last Updated:** YYYY-MM-DD

---

## Quick Navigation

### Sections

- [Core Java Fundamentals](#1-core-java-fundamentals)
- [Collections & Data Structures](#2-collections--data-structures)
- [Spring & Spring Boot](#3-spring--spring-boot)
- [Multithreading & Memory Management](#4-multithreading--memory-management)
- [Database & Hibernate](#5-database--hibernate)
- [Architecture & Design Patterns](#6-architecture--design-patterns)
- [Problem Solving & Coding Tasks](#7-problem-solving--coding-tasks)
- [Kafka & Messaging](#8-kafka--messaging)
- [Production Support & Troubleshooting](#9-production-support--troubleshooting)

### Quick Revision

- [Top P1 Questions](#top-p1-questions)
- [Recently Added Questions](#recently-added-questions)
- [Interview Notes](#interview-notes)

---

## Priority Legend

| Priority | Meaning |
|-----------|-----------|
| P1 | Very High Frequency |
| P2 | High Frequency |
| P3 | Medium Frequency |
| P4 | Low Frequency |

---

## Status Legend

- [Answered]
- [To be Answered]
- [Needs Revision]

---

## Question Template

> Copy this template whenever adding a new question.

```markdown
### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Real World Usage

#### Example

```java
// Code here
```
```

---

## Top P1 Questions

- Q169
- Q170
- Q174
- Q178
- Q181
- Q195
- Q196
- Q201
- Q217
- Q226

---

## Recently Added Questions

- Q150-Q235

---

# 1. Core Java Fundamentals

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 2. Collections & Data Structures

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 3. Spring & Spring Boot

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Real World Usage

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 4. Multithreading & Memory Management

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

---

# 5. Database & Hibernate

### Q194. First Level Cache vs Second Level Cache

**Priority:** P1
**Status:** Answered - Tuesday, 16 June 2026

#### Answer

# Q194. First Level Cache vs Second Level Cache

### One-Line Answer

**First Level Cache is a mandatory, session-scoped cache maintained by Hibernate for each persistence context, whereas Second Level Cache is an optional, shared cache across multiple sessions used to reduce database hits and improve application performance.**

---

## Detailed Explanation

Caching is one of the most important Hibernate performance optimization mechanisms.

When Hibernate fetches an entity from the database, it stores it in cache to avoid repeated database calls.

Hibernate provides two levels of caching:

### 1. First Level Cache (L1 Cache)

* Enabled by default.
* Associated with a Hibernate Session / JPA Persistence Context.
* Exists only during the lifetime of that session.
* Every entity loaded within a session is automatically stored in L1 cache.
* No additional configuration required.

Example:

```java
Employee emp1 = session.get(Employee.class, 1);
Employee emp2 = session.get(Employee.class, 1);
```

Only the first call hits the database.

The second call is served from First Level Cache.

---

### 2. Second Level Cache (L2 Cache)

* Optional.
* Shared across multiple sessions.
* Lives beyond a single session.
* Requires explicit configuration.
* Uses providers like:

  * Ehcache
  * Hazelcast
  * Infinispan
  * Caffeine

Example:

```java
Session session1 = sessionFactory.openSession();
Employee emp1 = session1.get(Employee.class, 1);
session1.close();

Session session2 = sessionFactory.openSession();
Employee emp2 = session2.get(Employee.class, 1);
```

Without L2 cache:

```text
DB Hit
DB Hit
```

With L2 cache:

```text
DB Hit
Cache Hit
```

---

## Internal Working / Execution Flow

### First Level Cache Flow

```text
Application
      |
      v
Hibernate Session
      |
      v
First Level Cache
      |
      +---- Entity Found -> Return
      |
      +---- Not Found
                  |
                  v
             Database
                  |
                  v
           Store in L1 Cache
```

---

### Second Level Cache Flow

```text
Application
      |
      v
Hibernate Session
      |
      v
L1 Cache
      |
      +---- Miss
      |
      v
L2 Cache
      |
      +---- Hit -> Return
      |
      +---- Miss
      |
      v
Database
      |
      v
Store in L2 Cache
Store in L1 Cache
```

---

## Real-World Usage

### Use First Level Cache

Always.

Since it is enabled automatically.

Typical scenario:

```text
Customer Service
-> Fetch Customer
-> Update Customer
-> Save Customer
```

Multiple accesses in the same transaction are served from L1 cache.

---

### Use Second Level Cache

When data:

* Changes infrequently
* Is read frequently
* Is shared by multiple users

Examples:

```text
Country List
Currency List
Product Categories
Tax Configurations
State Codes
Master Data
```

---

### Avoid L2 Cache For

```text
Stock Trading Data
Live Order Book
Real-time Pricing
Rapidly Changing Tables
```

Because cache invalidation becomes expensive.

---

## Advantages

### First Level Cache

* Enabled by default
* Improves transaction performance
* Prevents duplicate SQL execution
* Maintains entity consistency

### Second Level Cache

* Reduces database load
* Improves application throughput
* Shared across sessions
* Useful for read-heavy systems

---

## Disadvantages

### First Level Cache

* Scope limited to a single session
* Cleared when session closes
* Not shared across users

### Second Level Cache

* Additional configuration
* Cache invalidation complexity
* Potential stale data issues
* Extra memory consumption

---

## Alternatives / Competing Approaches

| Approach                    | Best Use Case                     |
| --------------------------- | --------------------------------- |
| First Level Cache           | Transaction-level caching         |
| Second Level Cache          | Shared application caching        |
| Redis                       | Distributed cache across services |
| Hazelcast                   | Cluster-wide caching              |
| Database Query Optimization | When caching is unnecessary       |
| Materialized Views          | Reporting workloads               |

---

## Code Example

### Enable Second Level Cache

```java
@Entity
@Cacheable
@org.hibernate.annotations.Cache(
    usage = CacheConcurrencyStrategy.READ_WRITE
)
public class Employee {

    @Id
    private Long id;

    private String name;
}
```

Application configuration:

```properties
spring.jpa.properties.hibernate.cache.use_second_level_cache=true
spring.jpa.properties.hibernate.cache.region.factory_class=org.hibernate.cache.jcache.JCacheRegionFactory
```

---

## Performance Considerations

### First Level Cache

* Lookup Complexity: O(1)
* Memory usage grows with session size.
* Large sessions can cause memory pressure.

---

### Second Level Cache

* Significantly reduces database round trips.
* Improves response time for frequently accessed data.
* Requires memory sizing and eviction strategies.

---

## Common Follow-Up Questions

1. Is First Level Cache enabled by default?
2. Can First Level Cache be disabled?
3. How is L1 cache implemented internally?
4. Is Second Level Cache enabled by default?
5. What cache providers are supported?
6. What is Query Cache?
7. Difference between Query Cache and L2 Cache?
8. How does cache eviction work?
9. What is CacheConcurrencyStrategy?
10. When should L2 cache not be used?

---

## Interview Traps & Misconceptions

### ❌ First Level Cache is shared across sessions.

Why wrong:

Each Hibernate Session has its own cache.

### ✅ Correct Answer

**No. First Level Cache is session-scoped and not shared between sessions.**

---

### ❌ Second Level Cache stores query results.

Why wrong:

L2 Cache stores entities.

Query results are handled separately by Query Cache.

### ✅ Correct Answer

**Second Level Cache stores entities, while Query Cache stores query result sets.**

---

### ❌ First Level Cache can be disabled globally.

Why wrong:

It is fundamental to Hibernate's persistence context.

### ✅ Correct Answer

**First Level Cache is mandatory and cannot be completely disabled.**

---

### ❌ L2 Cache should be enabled for all entities.

Why wrong:

Frequently changing entities create cache churn.

### ✅ Correct Answer

**L2 Cache should be used selectively for read-heavy, rarely changing entities.**

---

## Senior-Level Discussion Points

A 2–3 year developer typically knows:

* L1 cache exists
* L2 cache improves performance

A 5–8 year developer should additionally know:

* Persistence Context internals
* Entity state management
* Cache invalidation strategies
* Cache concurrency modes
* Query Cache vs Entity Cache
* Redis vs Hibernate L2 Cache
* Memory trade-offs
* Distributed caching considerations

---

## Quick Revision Notes

* L1 Cache = Session scoped.
* L1 Cache = Enabled by default.
* L1 Cache = Mandatory.
* L2 Cache = Shared across sessions.
* L2 Cache = Optional.
* L2 Cache requires configuration.
* L2 Cache best for read-heavy data.
* Query Cache ≠ L2 Cache.
* L1 checked before L2.
* L2 checked before DB.

---

## Interview Answer (60-Second Version)

Hibernate provides two cache levels. First Level Cache is session-scoped and enabled by default. Once an entity is loaded in a session, repeated fetches are served from the session cache without hitting the database. Second Level Cache is optional and shared across multiple sessions. It reduces database load by storing frequently accessed entities in a common cache provider like Ehcache or Hazelcast. L1 cache is mandatory, while L2 cache should be used selectively for read-heavy and infrequently changing data.

---

## Interview Answer (3-Minute Deep Dive Version)

First Level Cache is Hibernate's session-level cache and is enabled by default. Every Session maintains a Persistence Context that stores entities loaded during that session. If the same entity is requested again, Hibernate returns it directly from the cache without executing another SQL query.

Second Level Cache is a shared cache across multiple sessions and must be explicitly configured. When a session cannot find an entity in L1 cache, Hibernate checks L2 cache before hitting the database. This significantly improves performance for frequently accessed, relatively static data such as country codes, product categories, and configuration tables.

A key distinction is scope: L1 cache exists only within a session, while L2 cache is application-wide. Another important interview point is that L2 cache stores entities, whereas Query Cache stores query result sets. In production systems, L2 cache should be used selectively because cache invalidation and stale data management become important concerns for highly dynamic datasets.


[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

### Q204. Explain HikariCP.

**Priority:** P1
**Status:** Answered - Wednesday, 17 June 2026

#### Answer

# 204. Explain HikariCP. **[P1]**

## One-Line Answer

**HikariCP is a high-performance JDBC connection pool used to efficiently manage and reuse database connections, reducing connection creation overhead and improving application throughput.**

---

# Why Do We Need HikariCP?

Creating a database connection is an expensive operation.

Without connection pooling:

```text
Request 1
   ↓
Create Connection
   ↓
Execute Query
   ↓
Close Connection

Request 2
   ↓
Create Connection
   ↓
Execute Query
   ↓
Close Connection
```

For thousands of requests, constantly creating and destroying connections becomes very costly.

---

# What is HikariCP?

HikariCP is a **JDBC Connection Pool Implementation**.

Instead of creating new connections every time, it maintains a pool of pre-created connections.

```text
                    HikariCP Pool

                [Conn1]
                [Conn2]
Application --> [Conn3] --> Database
                [Conn4]
                [Conn5]
```

When a request needs a connection:

1. Borrow a connection from the pool.
2. Execute queries.
3. Return it to the pool.

The connection is reused rather than destroyed.

---

# Internal Working

### Without Pooling

```java
Connection con = DriverManager.getConnection(...);
```

Each request:

```text
Create TCP Connection
Authenticate
Allocate Resources
Execute Query
Close Connection
```

Very expensive.

---

### With HikariCP

```java
Connection con = dataSource.getConnection();
```

Internally:

```text
Pool Available?
      |
     Yes
      |
Return Existing Connection
      |
Execute Query
      |
Return Connection To Pool
```

No new database connection is created.

---

# Why is HikariCP Popular?

Compared to older pools such as:

* Apache DBCP
* C3P0
* Tomcat JDBC Pool

HikariCP offers:

### Faster Performance

Optimized code paths and minimal locking.

### Lower Memory Usage

Consumes less memory compared to older pools.

### Better Throughput

Handles large numbers of concurrent requests efficiently.

### Faster Startup

Creates and manages connections quickly.

---

# Spring Boot and HikariCP

Starting from Spring Boot 2.x, HikariCP became the **default connection pool**.

If dependency exists:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Spring Boot automatically configures HikariCP.

No extra setup required.

---

# Common HikariCP Configuration

```properties
spring.datasource.hikari.maximum-pool-size=20
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=30000
spring.datasource.hikari.idle-timeout=600000
spring.datasource.hikari.max-lifetime=1800000
```

---

# Important Configuration Parameters

## 1. Maximum Pool Size

```properties
spring.datasource.hikari.maximum-pool-size=20
```

Maximum number of connections allowed.

```text
Pool Capacity = 20
```

21st request waits until a connection becomes available.

---

## 2. Minimum Idle

```properties
spring.datasource.hikari.minimum-idle=5
```

Minimum idle connections maintained.

```text
Always Keep 5 Ready Connections
```

Improves response time.

---

## 3. Connection Timeout

```properties
spring.datasource.hikari.connection-timeout=30000
```

Maximum wait time to obtain a connection.

```text
30 Seconds
```

After timeout:

```java
SQLTransientConnectionException
```

is thrown.

---

## 4. Idle Timeout

```properties
spring.datasource.hikari.idle-timeout=600000
```

Unused connections are removed after the configured period.

---

## 5. Max Lifetime

```properties
spring.datasource.hikari.max-lifetime=1800000
```

Maximum lifetime of a connection before replacement.

Prevents stale database connections.

---

# Real-World Example

Suppose an e-commerce application receives:

```text
500 Requests Per Second
```

Without pooling:

```text
500 New DB Connections Every Second
```

Database may become overloaded.

With HikariCP:

```text
Pool Size = 50

500 Requests
      ↓
Reuse Same 50 Connections
      ↓
Serve Requests Efficiently
```

This dramatically reduces database overhead.

---

# HikariCP and Hibernate

Typical flow:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Hibernate/JPA
    ↓
HikariCP
    ↓
Database
```

Hibernate does not create database connections directly.

It requests them from HikariCP.

```text
Hibernate
      ↓
getConnection()
      ↓
HikariCP
      ↓
Returns Pooled Connection
```

---

# Advantages

### Advantages

* Extremely fast
* Lightweight
* Low latency
* Better throughput
* Production proven
* Default in Spring Boot
* Minimal configuration

---

### Disadvantages

* Incorrect pool sizing can cause bottlenecks.
* Too many connections can overload the database.
* Requires monitoring in high-traffic systems.

---

# Common Follow-Up Questions

### Q1. What problem does HikariCP solve?

Connection creation overhead by reusing database connections.

---

### Q2. Why is HikariCP faster than C3P0 or DBCP?

Optimized internal implementation, reduced locking, lower memory footprint, and efficient connection management.

---

### Q3. Is HikariCP a database?

No.

It is a JDBC connection pool.

---

### Q4. Does HikariCP replace Hibernate?

No.

```text
Hibernate → ORM Framework

HikariCP → Connection Pool
```

They solve different problems.

---

### Q5. What happens when all connections are busy?

Requests wait for an available connection.

If wait exceeds:

```properties
connection-timeout
```

an exception is thrown.

---

# Interview Traps / Misconceptions

### Trap 1

**"HikariCP improves query performance."**

Incorrect.

It does not make SQL queries faster.

It reduces the cost of obtaining database connections.

---

### Trap 2

**"HikariCP creates unlimited connections."**

Incorrect.

Pool size is limited by configuration.

---

### Trap 3

**"Each request gets a new database connection."**

Incorrect.

Connections are reused from the pool.

---

# Senior-Level Discussion Points

### Pool Sizing Strategy

A common mistake is:

```text
More Connections = Better Performance
```

Not always true.

Too many connections can:

* Increase DB contention
* Increase memory usage
* Reduce overall throughput

Pool size should be based on:

* Database capacity
* CPU cores
* Query execution time
* Concurrent workload

---

### Connection Leak Detection

HikariCP supports leak detection:

```properties
spring.datasource.hikari.leak-detection-threshold=30000
```

Useful for identifying connections that are borrowed but never returned.

---

### Monitoring

Metrics are often exposed through:

* JMX
* Micrometer
* Spring Boot Actuator

to track:

* Active connections
* Idle connections
* Waiting threads
* Pool utilization

---

# Quick Revision Notes

* HikariCP = JDBC Connection Pool.
* Default connection pool in Spring Boot.
* Reuses database connections instead of creating new ones.
* Improves throughput and reduces latency.
* Hibernate/JPA obtains connections from HikariCP.
* Key configs:

  * maximum-pool-size
  * minimum-idle
  * connection-timeout
  * idle-timeout
  * max-lifetime
* Faster and lighter than C3P0 and DBCP.

---

# 60-Second Interview Answer

> HikariCP is a high-performance JDBC connection pool used to efficiently manage database connections. Instead of creating a new connection for every request, it maintains a pool of reusable connections. When Hibernate or JPA needs a connection, it borrows one from the pool and returns it after use. This significantly reduces connection creation overhead, improves throughput, and lowers latency. HikariCP is lightweight, fast, and is the default connection pool in Spring Boot. Key configurations include maximum pool size, minimum idle connections, connection timeout, idle timeout, and max lifetime.

---

# 3-Minute Deep-Dive Answer

> HikariCP is a JDBC connection pooling library that improves application performance by reusing database connections. Creating a database connection involves network setup, authentication, and resource allocation, which are expensive operations. HikariCP maintains a pool of pre-created connections and hands them out to application threads when needed. Once the work is completed, the connection is returned to the pool rather than closed.
>
> In a Spring Boot application, Hibernate/JPA obtains connections from HikariCP. When traffic increases, the pool serves multiple requests using a fixed number of reusable connections, greatly reducing overhead. HikariCP is known for its low latency, minimal locking, efficient memory usage, and high throughput compared to older pools like C3P0 and Apache DBCP.
>
> Important configuration properties include `maximum-pool-size`, `minimum-idle`, `connection-timeout`, `idle-timeout`, and `max-lifetime`. Proper pool sizing is crucial because too few connections create bottlenecks while too many can overwhelm the database. In production systems, HikariCP is commonly monitored using Spring Boot Actuator, Micrometer, or JMX metrics.

[⬆ Back to Top](#java--spring-boot-interview-master-repository)


---

### Q195. Explain the N+1 Query Problem. 

**Priority:** P1
**Status:** Answered - Wednesday, 17 June 2026

#### Answer

# 195. Explain the N+1 Query Problem. **[P1]**

## One-Line Answer

**The N+1 Query Problem occurs when Hibernate executes one query to fetch parent entities and then executes N additional queries to fetch related child entities, causing significant performance degradation.**

---

# First Understand It in Layman Terms

Imagine you are a manager and want to see:

```text
All Departments
and
Employees in each Department
```

Suppose the database contains:

```text
Department A → 10 Employees
Department B → 8 Employees
Department C → 15 Employees
```

### Efficient Approach

Ask once:

```sql
Give me all departments with all employees
```

Result:

```text
1 Database Trip
```

---

### N+1 Approach

Ask:

```sql
Give me all departments
```

Database returns:

```text
Department A
Department B
Department C
```

Now for each department:

```sql
Give me employees of Department A
Give me employees of Department B
Give me employees of Department C
```

Total:

```text
1 Query (Departments)
+
3 Queries (Employees)
=
4 Queries
```

This is called:

```text
N + 1

1 Parent Query
+
N Child Queries
```

---

# Why is it Called N+1?

Suppose:

```text
100 Departments
```

Hibernate executes:

```text
1 Query → Load Departments

100 Queries → Load Employees
```

Total:

```text
101 Queries
```

Hence:

```text
N + 1
```

---

# Real Hibernate Example

## Entities

```java
@Entity
public class Department {

    @Id
    private Long id;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;
}
```

```java
@Entity
public class Employee {

    @Id
    private Long id;

    @ManyToOne
    private Department department;
}
```

---

## Repository Call

```java
List<Department> departments =
        departmentRepository.findAll();
```

Hibernate executes:

```sql
SELECT * FROM department;
```

Only one query so far.

---

## Later

```java
for (Department d : departments) {
    System.out.println(d.getEmployees().size());
}
```

Now Hibernate loads employees lazily.

For every department:

```sql
SELECT * FROM employee WHERE department_id=1;

SELECT * FROM employee WHERE department_id=2;

SELECT * FROM employee WHERE department_id=3;

...
```

This creates N additional queries.

---

# Actual Query Flow

Suppose 5 departments exist.

Hibernate executes:

```sql
SELECT * FROM department;
```

Then:

```sql
SELECT * FROM employee WHERE department_id=1;
SELECT * FROM employee WHERE department_id=2;
SELECT * FROM employee WHERE department_id=3;
SELECT * FROM employee WHERE department_id=4;
SELECT * FROM employee WHERE department_id=5;
```

Total:

```text
1 + 5 = 6 Queries
```

---

# Why Is It Dangerous?

Developers often test with:

```text
3 Departments
```

Only:

```text
4 Queries
```

No problem noticed.

Production:

```text
5000 Departments
```

Now:

```text
5001 Queries
```

Performance becomes terrible.

---

# Common Cause: Lazy Loading

Default Hibernate behavior:

```java
@OneToMany(fetch = FetchType.LAZY)
```

Hibernate loads:

```text
Department
```

but delays loading:

```text
Employees
```

until:

```java
department.getEmployees()
```

is called.

This is where N+1 often occurs.

---

# Visual Representation

```text
Application
      |
      | findAll()
      v

Query #1
SELECT * FROM department

      |
      |
      v

Department 1
      |
      v

Query #2
SELECT * FROM employee
WHERE department_id=1

Department 2
      |
      v

Query #3
SELECT * FROM employee
WHERE department_id=2

Department 3
      |
      v

Query #4
SELECT * FROM employee
WHERE department_id=3
```

---

# How to Detect N+1?

Enable SQL logging:

```properties
spring.jpa.show-sql=true
```

or

```properties
logging.level.org.hibernate.SQL=DEBUG
```

If you see:

```text
1 parent query
followed by
many similar child queries
```

you likely have an N+1 problem.

---

# Solutions

## Solution 1: JOIN FETCH (Most Common)

### JPQL

```java
@Query("""
       SELECT d
       FROM Department d
       JOIN FETCH d.employees
       """)
List<Department> findAllWithEmployees();
```

Hibernate generates:

```sql
SELECT d.*, e.*
FROM department d
JOIN employee e
ON d.id = e.department_id;
```

Now:

```text
Only One Query
```

---

## Solution 2: Entity Graph

```java
@EntityGraph(attributePaths = "employees")
List<Department> findAll();
```

Tells Hibernate:

```text
Load employees together
```

---

## Solution 3: Batch Fetching

```properties
hibernate.default_batch_fetch_size=50
```

Instead of:

```sql
SELECT * FROM employee WHERE department_id=1;
SELECT * FROM employee WHERE department_id=2;
SELECT * FROM employee WHERE department_id=3;
```

Hibernate can execute:

```sql
SELECT *
FROM employee
WHERE department_id IN (1,2,3,...50);
```

Much fewer queries.

---

## Solution 4: DTO Projection

Load only required data.

```java
@Query("""
SELECT new com.app.DepartmentDTO(
       d.id,
       d.name)
FROM Department d
""")
```

Avoids loading unnecessary entities.

---

# Important Interview Trap

### Does EAGER Fetch Solve N+1?

Many developers think:

```java
fetch = FetchType.EAGER
```

solves N+1.

Not necessarily.

Hibernate may still execute:

```text
1 Parent Query
+
N Child Queries
```

depending on the query and mapping.

---

### Interview Statement

> EAGER fetching is not a guaranteed solution for the N+1 problem. JOIN FETCH or EntityGraph are preferred solutions.

---

# Internal Working

When Hibernate loads:

```java
List<Department> departments
```

it stores Department entities in the Persistence Context.

Employees are represented by proxies.

```text
Persistence Context

Department 1
Department 2
Department 3

Employees = Not Loaded Yet
```

When:

```java
department.getEmployees()
```

is called,

Hibernate initializes the proxy and fires another SQL query.

Doing this repeatedly creates N+1 queries.

---

# Advantages of Solving N+1

* Fewer database round trips
* Reduced latency
* Lower DB load
* Better scalability
* Faster API response times

---

# Common Follow-Up Questions

### Q1. What causes N+1?

Lazy loading of related entities.

---

### Q2. How do you identify N+1?

SQL logs, Hibernate statistics, APM tools.

---

### Q3. Best solution?

Usually:

```java
JOIN FETCH
```

or

```java
@EntityGraph
```

---

### Q4. Is N+1 only a Hibernate issue?

No.

Any ORM:

* Hibernate
* JPA
* Entity Framework
* Django ORM
* Sequelize

can suffer from it.

---

### Q5. Can ManyToOne also cause N+1?

Yes.

Example:

```java
List<Employee> employees = employeeRepo.findAll();
```

Then:

```java
employee.getDepartment();
```

for each employee can trigger N+1.

---

# Interview Traps / Misconceptions

### Trap 1

**"Lazy loading is bad."**

Incorrect.

Lazy loading is useful.

Improper usage causes N+1.

---

### Trap 2

**"EAGER always fixes N+1."**

Incorrect.

EAGER can sometimes create even more queries.

---

### Trap 3

**"N+1 is a Hibernate bug."**

Incorrect.

It's a query design and fetching strategy problem.

---

# Senior-Level Discussion Points

### JOIN FETCH vs Batch Fetching

**JOIN FETCH**

```text
Pros:
- Single query
- Simple

Cons:
- Large result sets
- Duplicate rows
```

---

**Batch Fetching**

```text
Pros:
- Less memory
- Better for huge datasets

Cons:
- Multiple queries still occur
```

---

### Production Monitoring

Monitor:

* Query count
* Query execution time
* Hibernate statistics
* Slow query logs

N+1 issues are often responsible for APIs that suddenly become slow at scale.

---

# Quick Revision Notes

* N+1 = 1 parent query + N child queries.
* Commonly caused by Lazy Loading.
* Major performance anti-pattern.
* Detected through SQL logs.
* Best fixes:

  * JOIN FETCH
  * EntityGraph
  * Batch Fetching
  * DTO Projection
* EAGER fetching is not a guaranteed fix.

---

# 60-Second Interview Answer

> The N+1 Query Problem occurs when Hibernate executes one query to load parent entities and then executes an additional query for each parent entity to load its related child entities. For example, fetching 100 departments and then lazily loading employees for each department can result in 101 SQL queries. This causes excessive database round trips and poor performance. Common solutions include using JOIN FETCH, EntityGraph, batch fetching, or DTO projections. It is one of the most common Hibernate performance issues.

---

# 3-Minute Deep-Dive Answer

> The N+1 Query Problem is a performance issue in Hibernate where a single query loads a collection of parent entities, and then Hibernate executes an additional query for each parent entity when related data is accessed. This often happens with lazy-loaded associations. For example, loading all departments may execute one query, but accessing employees for each department may trigger separate queries per department. If there are 100 departments, Hibernate can generate 101 SQL queries.
>
> The problem increases database round trips, response times, and overall system load. It is typically identified by enabling Hibernate SQL logs and observing repeated similar queries. The most common solutions are JPQL JOIN FETCH queries, JPA EntityGraph, Hibernate batch fetching, and DTO projections. While lazy loading often exposes the issue, eager fetching is not a guaranteed fix because Hibernate may still generate multiple queries depending on the query structure. Senior developers usually balance JOIN FETCH and batch fetching based on data volume and memory considerations.

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

### Q203. What is Connection Pooling?.

**Priority:** P1
**Status:** Answered - Wednesday, 17 June 2026

#### Answer

# 203. What is Connection Pooling? **[P1]**

## One-Line Answer

**Connection Pooling is a technique where a set of pre-created database connections are maintained and reused by applications, avoiding the overhead of creating and closing connections for every database request.**

---

# First Understand It in Layman Terms

Imagine a company has 500 employees and only 20 taxis available.

### Without Pooling

Every employee:

```text
Needs Taxi
     ↓
Buy New Taxi
     ↓
Use Taxi
     ↓
Destroy Taxi
```

This is extremely expensive and slow.

---

### With Pooling

Company keeps:

```text
20 Taxis Ready
```

Whenever someone needs one:

```text
Take Taxi
Use Taxi
Return Taxi
```

No need to buy a new taxi every time.

This is exactly how **Connection Pooling** works.

---

# Why Do We Need Connection Pooling?

Creating a database connection is expensive because it involves:

```text
Application
      ↓
Network Connection
      ↓
TCP Handshake
      ↓
Authentication
      ↓
Session Creation
      ↓
Resource Allocation
      ↓
Database Connection Ready
```

This may take milliseconds, but under thousands of requests it becomes significant.

---

# Without Connection Pooling

Suppose 1000 users hit your application.

For every request:

```java
Connection con =
    DriverManager.getConnection(...);
```

Flow:

```text
Request 1
Create Connection
Execute Query
Close Connection

Request 2
Create Connection
Execute Query
Close Connection

Request 3
Create Connection
Execute Query
Close Connection
```

Database spends a lot of time creating and destroying connections.

---

# With Connection Pooling

Application startup:

```text
Create 10 Connections
Store in Pool
```

```text
Connection Pool

[Conn1]
[Conn2]
[Conn3]
[Conn4]
[Conn5]
...
```

When request arrives:

```text
Borrow Connection
Execute Query
Return Connection
```

Connection is reused.

No creation cost.

---

# Internal Working

## Step 1: Application Starts

Pool creates connections:

```text
Pool

Conn1
Conn2
Conn3
Conn4
Conn5
```

---

## Step 2: Request Comes

```java
Connection con =
    dataSource.getConnection();
```

Pool returns:

```text
Conn1
```

---

## Step 3: Query Executes

```java
PreparedStatement ps =
    con.prepareStatement(...);
```

---

## Step 4: Close Connection

```java
con.close();
```

Important:

Many developers think:

```text
Connection Destroyed
```

Wrong.

In pooled environments:

```text
Connection Returned To Pool
```

---

# Visual Flow

```text
                Connection Pool

            [Conn1]
            [Conn2]
Request ---> [Conn3] ---> Database
            [Conn4]
            [Conn5]

After Use

Request ----> Return Conn3 To Pool
```

---

# Connection Pool vs Database Connection

### Database Connection

Actual physical connection to DB.

```text
Application
      ↔
Database
```

---

### Connection Pool

Manager that maintains multiple connections.

```text
Application
      ↓
Connection Pool
      ↓
Database
```

---

# Common Connection Pool Implementations

### HikariCP

Most popular today.

```text
Spring Boot Default
```

Fastest and lightweight.

---

### Apache DBCP

Older Apache implementation.

---

### C3P0

Older Hibernate-era pool.

---

### Tomcat JDBC Pool

Used in Tomcat environments.

---

# Connection Pooling in Spring Boot

Default implementation:

```text
HikariCP
```

Dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>
        spring-boot-starter-data-jpa
    </artifactId>
</dependency>
```

Spring Boot automatically configures HikariCP.

---

# Important Pool Configuration

## Maximum Pool Size

```properties
spring.datasource.hikari.maximum-pool-size=20
```

Maximum connections allowed.

```text
Pool Capacity = 20
```

---

## Minimum Idle

```properties
spring.datasource.hikari.minimum-idle=5
```

Always keep at least 5 ready connections.

---

## Connection Timeout

```properties
spring.datasource.hikari.connection-timeout=30000
```

Maximum wait time for a free connection.

---

## Idle Timeout

```properties
spring.datasource.hikari.idle-timeout=600000
```

Remove unused connections after a period.

---

## Max Lifetime

```properties
spring.datasource.hikari.max-lifetime=1800000
```

Replace old connections periodically.

---

# Real-World Example

Suppose:

```text
500 Requests Per Second
```

### Without Pooling

```text
500 New Connections Created Every Second
```

Heavy load on DB.

---

### With Pooling

```text
Pool Size = 50
```

```text
500 Requests
      ↓
Reuse Same 50 Connections
      ↓
Serve Requests Efficiently
```

Huge performance improvement.

---

# Connection Pooling and Hibernate

Flow:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Hibernate/JPA
    ↓
Connection Pool
    ↓
Database
```

Hibernate asks pool for a connection.

```java
Session session
```

Internally:

```text
Session
    ↓
DataSource
    ↓
Connection Pool
    ↓
Database Connection
```

---

# Advantages

### Performance Improvement

Avoids repeated connection creation.

---

### Better Scalability

Handles more concurrent users.

---

### Lower Database Overhead

Fewer connection creations.

---

### Faster Response Time

Connections already available.

---

### Resource Management

Limits number of active DB connections.

---

# Disadvantages

### Incorrect Pool Size

Too small:

```text
Threads Wait
```

Too large:

```text
Database Overloaded
```

---

### Memory Usage

Idle connections consume resources.

---

### Requires Monitoring

Need to track:

* Active connections
* Idle connections
* Wait times

---

# Common Follow-Up Questions

### Q1. Why is connection creation expensive?

Because it involves:

* Network communication
* Authentication
* Session creation
* Resource allocation

---

### Q2. What happens when pool is exhausted?

Requests wait.

If timeout exceeds:

```text
ConnectionTimeout
```

exception occurs.

---

### Q3. Does close() destroy the connection?

In pooled environments:

```java
connection.close();
```

returns it to the pool.

It usually does not destroy the physical connection.

---

### Q4. What is the default pool in Spring Boot?

**HikariCP**

---

### Q5. Is connection pooling part of Hibernate?

No.

Hibernate uses a pool but does not implement connection pooling itself.

---

# Interview Traps / Misconceptions

### Trap 1

**"Connection pooling makes SQL queries faster."**

Incorrect.

It reduces connection creation overhead.

Poor SQL remains poor SQL.

---

### Trap 2

**"More connections always mean better performance."**

Incorrect.

Too many connections can reduce performance and overwhelm the database.

---

### Trap 3

**"close() closes the physical connection."**

In pooled environments, it usually returns the connection to the pool.

---

# Senior-Level Discussion Points

## Pool Sizing

A common production mistake:

```text
Database CPU = 8 cores

Pool Size = 500
```

This often performs worse than:

```text
Pool Size = 20–50
```

because of DB contention.

---

## Connection Leaks

Bad code:

```java
Connection con =
    dataSource.getConnection();
```

Never returned.

Eventually:

```text
Pool Exhausted
```

No connections available.

---

## Monitoring Metrics

Track:

* Active connections
* Idle connections
* Borrow time
* Wait time
* Pool utilization

Using:

* Spring Boot Actuator
* Micrometer
* JMX

---

# Quick Revision Notes

* Connection Pooling = Reuse DB connections.
* Avoids expensive connection creation.
* Improves performance and scalability.
* Connection borrowed → used → returned.
* `close()` usually returns connection to pool.
* Spring Boot default pool = HikariCP.
* Important configs:

  * maximum-pool-size
  * minimum-idle
  * connection-timeout
  * idle-timeout
  * max-lifetime

---

# 60-Second Interview Answer

> Connection Pooling is a technique used to maintain a pool of reusable database connections instead of creating and destroying connections for every request. Creating a database connection is expensive because it involves network setup and authentication. A connection pool pre-creates connections and allows applications to borrow and return them as needed. This improves performance, scalability, and resource utilization. In Spring Boot, HikariCP is the default connection pool implementation. Key configuration properties include maximum pool size, minimum idle connections, and connection timeout.

---

# 3-Minute Deep-Dive Answer

> Connection Pooling is a resource management technique that improves database performance by reusing existing database connections. Without pooling, every request creates a new connection, executes queries, and closes the connection, which is expensive due to network communication, authentication, and session initialization. A connection pool maintains a set of pre-created connections. When an application needs a database connection, it borrows one from the pool and returns it after use. This significantly reduces latency and increases throughput.
>
> In modern Spring Boot applications, HikariCP is the default connection pool. Hibernate and JPA obtain connections from the pool rather than creating them directly. Important configuration parameters include maximum pool size, minimum idle connections, connection timeout, idle timeout, and max lifetime. Proper pool sizing is critical because too few connections create bottlenecks while too many can overload the database. Monitoring connection pool metrics and preventing connection leaks are important production considerations.

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

### Q196. What is Dirty Checking in Hibernate? .

**Priority:** P1
**Status:** Answered - Wednesday, 17 June 2026

#### Answer

# 196. What is Dirty Checking in Hibernate? **[P1]**

## One-Line Answer

**Dirty Checking is a Hibernate mechanism that automatically detects changes made to managed entities and synchronizes those changes with the database during flush or transaction commit.**

---

# First Understand It in Layman Terms

Imagine your manager gives you a document for editing.

When you receive it:

```text
Original Document
Salary = 50000
```

The manager secretly keeps a copy.

You edit:

```text
Salary = 70000
```

Before saving, the manager compares:

```text
Original Copy = 50000
Current Copy  = 70000
```

Manager notices:

```text
Something changed!
```

and updates the official record.

This is exactly what Hibernate does.

---

# Why is it Called Dirty Checking?

In Hibernate terminology:

```text
Clean Object
```

means:

```text
No changes made
```

Example:

```java
Employee emp = session.get(Employee.class, 1L);
```

Immediately after loading:

```text
Employee = Clean
```

---

When you modify it:

```java
emp.setSalary(70000);
```

Hibernate marks it as:

```text
Dirty
```

Meaning:

```text
Current State != Original State
```

The process of detecting this difference is called:

## Dirty Checking

---

# Real Hibernate Example

## Step 1: Load Entity

```java
Session session = sessionFactory.openSession();

Employee emp =
    session.get(Employee.class, 1L);
```

Hibernate executes:

```sql
SELECT * FROM employee
WHERE id = 1;
```

Suppose:

```text
ID = 1
Name = John
Salary = 50000
```

Hibernate stores internally:

```text
Persistence Context

Employee#1
Original Salary = 50000
```

---

## Step 2: Modify Entity

```java
emp.setSalary(70000);
```

No SQL executes.

Database still contains:

```text
Salary = 50000
```

---

## Step 3: Commit Transaction

```java
transaction.commit();
```

Hibernate compares:

```text
Original Salary = 50000
Current Salary  = 70000
```

Difference detected.

Hibernate automatically generates:

```sql
UPDATE employee
SET salary = 70000
WHERE id = 1;
```

You never called:

```java
session.update(emp);
```

Hibernate handled it automatically.

---

# Internal Working

When Hibernate loads an entity:

```java
Employee emp =
    session.get(Employee.class, 1L);
```

It stores:

### Entity Object

```text
Employee Object
```

and

### Snapshot

```text
Original State Snapshot

id=1
name=John
salary=50000
```

Inside the Persistence Context.

---

Later:

```java
emp.setSalary(70000);
```

Current object becomes:

```text
id=1
name=John
salary=70000
```

At flush time:

```text
Snapshot
      vs
Current Object
```

Comparison happens.

If different:

```text
Entity is Dirty
```

Generate UPDATE SQL.

---

# Visual Representation

```text
Database
   |
   | SELECT
   v

Employee(50000)

        ↓

Persistence Context

Current Object = 50000
Snapshot       = 50000

        ↓

emp.setSalary(70000)

        ↓

Current Object = 70000
Snapshot       = 50000

        ↓

Dirty Checking

        ↓

UPDATE employee
SET salary=70000
```

---

# When Does Dirty Checking Occur?

Usually during:

### Flush

```java
session.flush();
```

---

### Transaction Commit

```java
transaction.commit();
```

Commit automatically triggers flush.

---

# Example with Flush

```java
emp.setSalary(70000);

session.flush();
```

Hibernate immediately executes:

```sql
UPDATE employee
SET salary=70000
WHERE id=1;
```

without waiting for commit.

---

# Dirty Checking and Persistence Context

This is one of the most important interview points.

Dirty Checking works only for entities that are:

```text
Managed
```

by the Persistence Context.

---

## Managed Entity

```java
Employee emp =
    session.get(Employee.class, 1L);
```

Hibernate tracks it.

Dirty Checking works.

---

## Detached Entity

```java
session.close();

emp.setSalary(70000);
```

Now Hibernate is no longer tracking it.

Dirty Checking will NOT happen.

No update SQL is generated.

---

# Example

```java
Session session =
        sessionFactory.openSession();

Employee emp =
        session.get(Employee.class, 1L);

session.close();

emp.setSalary(70000);
```

Result:

```text
No Dirty Checking
No UPDATE Query
```

because entity became:

```text
Detached
```

---

# Entity Lifecycle and Dirty Checking

| State              | Dirty Checking Works? |
| ------------------ | --------------------- |
| Transient          | ❌ No                  |
| Persistent/Managed | ✅ Yes                 |
| Detached           | ❌ No                  |
| Removed            | N/A                   |

---

# Dirty Checking vs Explicit Update

## Without Dirty Checking

Developer must write:

```java
Employee emp =
        employeeRepo.findById(1);

emp.setSalary(70000);

session.update(emp);
```

---

## With Dirty Checking

Only:

```java
Employee emp =
        session.get(Employee.class, 1);

emp.setSalary(70000);
```

Hibernate handles the update automatically.

---

# Performance Considerations

Dirty Checking is convenient but not free.

For every managed entity Hibernate may compare:

```text
Snapshot
     vs
Current State
```

before flush.

If Persistence Context contains:

```text
50,000 Entities
```

Dirty Checking becomes expensive.

---

# Optimization Techniques

## Read-Only Transactions

```java
@Transactional(readOnly = true)
```

Reduces unnecessary Dirty Checking.

---

## Detach Unused Entities

```java
session.detach(entity);
```

Stops Hibernate from tracking them.

---

## Clear Persistence Context

```java
session.clear();
```

Removes all managed entities.

Useful in batch processing.

---

# Common Follow-Up Questions

### Q1. Does Dirty Checking require session.update()?

No.

Hibernate automatically detects changes.

---

### Q2. When is UPDATE SQL generated?

During:

```text
Flush
or
Commit
```

---

### Q3. Does Dirty Checking work on detached entities?

No.

Only managed entities are tracked.

---

### Q4. Where does Hibernate keep the original values?

In a snapshot stored inside the Persistence Context.

---

### Q5. What enables Dirty Checking?

The Persistence Context (First-Level Cache).

Without it Hibernate cannot track changes.

---

# Interview Traps / Misconceptions

### Trap 1

**"Calling setter immediately updates the database."**

Incorrect.

```java
emp.setSalary(70000);
```

only changes the Java object.

SQL executes later during flush/commit.

---

### Trap 2

**"Dirty Checking works after session is closed."**

Incorrect.

Detached entities are not tracked.

---

### Trap 3

**"Dirty Checking updates all entities."**

Incorrect.

Only modified managed entities are updated.

---

# Senior-Level Discussion Points

## Snapshot-Based Dirty Checking

Hibernate traditionally keeps snapshots:

```text
Original State
```

and compares them at flush time.

---

## Enhanced Dirty Tracking (Bytecode Enhancement)

Modern Hibernate can use bytecode enhancement.

Instead of comparing every field:

```text
Snapshot Comparison
```

Hibernate knows exactly:

```text
Field X Changed
```

which improves performance.

---

## Large Persistence Contexts

Common production issue:

```text
Thousands of Managed Entities
```

Dirty Checking overhead increases.

Solutions:

* Batch processing
* session.clear()
* StatelessSession
* Read-only transactions

---

# Quick Revision Notes

* Dirty Checking = Automatic change detection.
* Works only on managed entities.
* Uses snapshots stored in Persistence Context.
* UPDATE generated during flush/commit.
* No explicit update() call needed.
* Detached entities are not tracked.
* Core feature of Hibernate ORM.

---

# 60-Second Interview Answer

> Dirty Checking is a Hibernate mechanism that automatically detects modifications made to managed entities. When an entity is loaded, Hibernate stores its original state in the Persistence Context. Before flush or commit, Hibernate compares the current entity state with the stored snapshot. If differences are found, Hibernate generates the required UPDATE SQL automatically. Dirty Checking works only for managed entities and is one of the key features that reduces the need for explicit update operations.

---

# 3-Minute Deep-Dive Answer

> Dirty Checking is Hibernate's automatic change detection mechanism. When an entity is loaded into the Persistence Context, Hibernate stores a snapshot of its original state. If the application modifies the entity while it remains managed, Hibernate compares the current state with the snapshot during flush or transaction commit. If changes are detected, Hibernate generates the necessary UPDATE statements automatically. This eliminates the need for explicit update calls and simplifies data persistence.
>
> Dirty Checking depends on the Persistence Context because Hibernate can only track entities that are currently managed. Detached entities are not monitored, so modifications to them are ignored unless they are reattached. Internally, Hibernate traditionally uses snapshot comparison, though newer versions can use bytecode enhancement for more efficient field-level tracking. While Dirty Checking improves developer productivity, large Persistence Contexts can increase comparison overhead, making techniques like read-only transactions, session clearing, and batch processing important in high-performance applications.

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

### Q196. What is Dirty Checking in Hibernate? .

**Priority:** P1
**Status:** Answered - Wednesday, 17 June 2026

#### Answer


[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

---

# 6. Architecture & Design Patterns

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Real World Usage

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 7. Problem Solving & Coding Tasks

### Q<Number>. <Problem Statement>

**Status:** Answered / To be Answered / Needs Revision

#### Approach

#### Solution

```java
// Code here
```

#### Time Complexity

#### Space Complexity

#### Alternative Approaches

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 8. Kafka & Messaging

### Q<Number>. <Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Key Points

#### Common Follow-up Questions

#### Example

```java
// Code here
```

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# 9. Production Support & Troubleshooting

### Q<Number>. <Scenario Question>

**Priority:** P1/P2/P3/P4  
**Status:** Answered / To be Answered / Needs Revision

#### Answer

#### Investigation Steps

#### Logs to Check

#### Metrics to Check

#### Root Cause Analysis

#### Resolution

#### Real World Notes

[⬆ Back to Top](#java--spring-boot-interview-master-repository)

---

# Interview Notes

## Recently Asked Questions

## Company Specific Questions

## Weak Areas

## Revision Notes

---