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

## psql
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

