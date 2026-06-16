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