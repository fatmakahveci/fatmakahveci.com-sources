---
title: Database
description: Database
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "nosql"
  - "sql"
  - "coding"
  - "database"
---

## Database Management Systems (DBMS)

### 1. NoSQL

- NoSQL is a class of DBMs that are non-relational and generally do not use SQL.
- It allows the representation of alternative structures, encouraging greater flexibility.
- NoSQL lacks the standard interface which SQL provides, so more complex queries can be difficult to execute.
- i.e. mongoDB, Cassandra, DynamoDB, Apache CouchDB, Redis, InfinityDB, MariaDB, Scylla, ArangoDB, InfiniteGraph, Neo4j, etc.
- It is preferred for
  - graph or hierarchical data.
  - data sets which are both large and mutate significantly.
  - businesses growing extremely fast, but lacking data schemata.
- It can be scaled vertically, by increasing the power of existing hardware.
- NoSQL databases need not stick to a strict format, but generally fit into one of four broad categories:
  1. **Column-oriented DBs** transpose row-oriented RDBMSs, allowing efficient storage of high-dimensional data and individual records with varying attributes.
  2. **Key-Value** stores are dictionaries which access diverse objects with a key unique to each.
  3. **Document** stores hold semi-structured data: objects which contain all of their relevant information, and which can be completely different from each other.
  4. **Graph** databases add the concept of relationships (direct links between objects) to documents, allowing rapid traversal of greatly connected data sets.
- NoSQL technologies adhere to the “CAP” theorem, which says that in any distributed database, only two of the following properties can be guaranteed at once:
  1. **Consistency:** Every request receives the most recent result or an error. (Note this is different than in ACID)
  2. **Availability:** Every request has a non-error result, regardless of how recent that result is.
  3. **Partition tolerance:** Any delays or losses between nodes will not interrupt the system’s operation.

### 2. SQL

- SQL is the PL used to interface with relational DBs.
- Declarative (Bildirimsel)
- It is particularly well-suited for complex queries.
- It is preferred when the data is
  - small.
  - conceptually modelled as tabular.
  - in systems where consistency is critical.
- It uses a master-slave architecture so
  - It can be scaled by adding more power to the current machines.
- SQL database schemata always represent relational, tabular data, with rules about consistency and integrity. They contain tables with columns (attributes) and rows (records), and keys have constrained logical relationships.
- RDBMSs must exhibit four “ACID” properties:
  1. **Atomicity** means all transactions must succeed or fail. They cannot be partially complete, even in the case of system failure.
  2. **Consistency** means that at each step the database follows invariants: rules which validate and prevent corruption.
  3. **Isolation** prevents concurrent transactions from affecting each other. Transactions must result in the same final state as if they were run sequentially, even if they were run in parallel.
  4. **Durability** makes transactions final. Even system failure cannot roll back the effects of a successful transaction.

### 2.1. Relational DBMS

- CRUD:= CREATE READ UPDATE DELETE

- i.e. **PostgreSQL:** An object-relational DBMS

  ```bash
  brew install postgresql
  brew services start postgresql
  brew services stop postgresql
  brew postgresql-upgrade-database
  ```

  - **pgADMIN (GUI)** `https://www.pgadmin.org/download/`
