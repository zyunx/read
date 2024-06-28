# Overview of PostgreSQL Internals

# 50.1 The Path of a Query

1. Connecting

2. Parsing to produce a query tree

3. Rule System

4. Plannner/Optimizor

5. Executing

# 50.2 How Connections are Established

PostgreSQL is implemented using a simple "process per user" client/server model.

The master process is *postgres*.
The master process spawn a new worker process for each connection.

# 50.3 The Parser Stage

## 50.3.1 Parser

scan.l using flex
gram.y using bison

## 50.3.2 Transforming Process

Transforming process takes the parser tree handed back by the parser
as input and does semantic interpretation needed to understand
which tables, functions, and operators are refrenced by the query.

The process can only be done within a transaction.

## 50.4 The PosgreSQL Rule System

query rewriting

## 50.5 Planner/Optimizor

### 50.5.1 Generating Possible Plans

1. generating plans for scanning each individual relation

    1. sequential scan
    2. index scan(WHERE clause and ORDER BY clause)

2. plans for joining relations

    1. nested loop join
    2. merge join
    3. hash join

3. attach selection and projection expressions

## 50.6 Executor

demand-pull pipeline mechanism

ModifyTable for INSERT, UPDATE, DELETE.
