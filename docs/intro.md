---
sidebar_position: 1
---

# intro
commands have so many permutations
- simplest and most useful commands are provided in this tutorial
## PostgreSQL version
```jsx title="bash"
$ postgres -V
$ psql -V
```

## PostgreSQL config files
```jsx title="bash"
$ sudo -u postgres psql -c "SHOW config_file;"
$ sudo -u postgres psql -c "SHOW hba_file;"
```

## changing postgresql user password
```jsx title="bash"
ALTER USER postgres WITH PASSWORD 'new_strong_password';
```

## granting privileges to a user
``` jsx title="sql"
GRANT CONNECT ON DATABASE gnostexdb TO gnostex;
GRANT USAGE ON SCHEMA public TO gnostex;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO gnostex;
 
```

## psql - PostgreSQL client
most common way to send queries to your PostgreSQL is using the provided psql client

### full connection format
```jsx title="bash"
psql -h <host> -p <port> -U <user> -d <database>
```

## connection URI 
``` jsx title="useful for scripts & Docker"
psql postgresql://user:password@host:port/database

ex.
psql postgresql://appuser:secret@localhost:5432/myapp

```

## connection using environment variables

```jsx title="bash"
export PGUSER=appuser
export PGDATABASE=myapp
export PGHOST=localhost
export PGPORT=5432

# then simply run
$psql
```
1. Table Inheritance (OO-like behavior)

Native parent/child table relationships.

Queries on a parent can automatically include child tables.

Supports polymorphism in SQL queries.

Other RDBMS require manual joins, unions, or table-per-type patterns to achieve the same.

2. Advanced indexing options

Multiple index types: B-tree, GIN, GiST, BRIN.

Supports full-text search, array, JSONB, and geospatial data indexes.

Partial and expression-based indexes.

Most RDBMS only offer simple B-tree indexes.

3. Extensible data types

Supports native arrays, JSON/JSONB, HSTORE, ranges, UUIDs, and custom types.

You can create your own user-defined types and functions.

4. Procedural language and triggers

Supports PL/pgSQL, PL/Python, PL/Perl, and more.

Powerful triggers and rules for automated behaviors.

You can implement complex business logic directly in the database.

5. Advanced constraints and expressions

CHECK constraints with expressions.

Exclusion constraints (e.g., no overlapping ranges).

Foreign keys, partial unique constraints, and deferrable constraints.

6. Concurrency and transaction model

MVCC (Multi-Version Concurrency Control) for highly concurrent workloads.

Fine-grained control over transaction isolation levels.

7. Extensibility

Add custom functions, operators, index types, aggregates.

Create domains (custom data types with constraints).

Support for procedural logic and extensions like PostGIS for GIS.

Conclusion

PostgreSQL isn’t just a relational database — it’s feature-rich, extensible, and highly capable, often compared to “enterprise-grade” RDBMS like Oracle or SQL Server.

Table inheritance, advanced indexing, extensible types, and powerful procedural features are just a few examples that make PostgreSQL an advanced RDBMS.
