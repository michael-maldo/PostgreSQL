---
sidebar_position: 1
---

# sql - intro
these commands are sequential<br/>
creates db, schema, sets search_path, creates and populates tables<br/>
then follows with queries, joins<br/>


## initialize basicsdb database
-- if db EXISTS, DROP it first
```jsx title="sql"
DROP DATABASE IF EXISTS basicsdb; 

CREATE DATABASE basicsdb;
\c basicsdb
```

## add basics schema
```jsx title="sql"
CREATE SCHEMA IF NOT EXISTS basics;
SET search_path TO basics, public;
show search_path;
```

## creating a new table
```jsx title="sql"
DROP TABLE IF EXISTS weather;
CREATE TABLE IF NOT EXISTS weather (
    city varchar(80),
    temp_lo int,
    temp_hi int,
    prcp real,
    cur_date date
);

CREATE TABLE cities (
    name            varchar(80),
    location        point
);

\d weather;
```

## populating a table with rows

```jsx title='sql"
INSERT INTO weather VALUES ('San Francisco', 1, 50, 0.25, '1994-11-27');
INSERT INTO weather VALUES ('New York', 2, 50, 0.25, '1994-11-27');
SELECT * FROM weather;
COPY weather FROM '/var/lib/pgsql/scripts/weather.txt';
SELECT * FROM weather;
COPY weather TO '/var/lib/pgsql/scripts/weather.copy.txt';


INSERT INTO cities VALUES ( 'San Francisco', '(-122.4194, 37.7794)');
INSERT INTO cities VALUES ( 'New York', '(-74.0060, 40.7128)');

\echo SELECT * FROM cities;
SELECT * FROM cities;


\dt basics.*

\d basics.*
```

## querying a table

### SELECT *

```jsx title="sql"
\echo SELECT * FROM weather;
SELECT * FROM weather;

\echo SELECT city, temp_lo, temp_hi, prcp, cur_date FROM weather;
SELECT city, temp_lo, temp_hi, prcp, cur_date FROM weather;
```

### you can write expressions
not just simple column references, in the SELECT list.

```jsx title="sql"
\echo SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, cur_date FROM weather;
\echo

SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, cur_date FROM weather;
```



### a query can be “qualified”
by adding a WHERE clause that specifies which rows are wanted.<br /> 
The WHERE clause contains a Boolean (truth value) expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (AND, OR, and NOT) are allowed in the qualification

```jsx title="sql"
\echo
\echo SELECT * FROM weather WHERE city = 'San Francisco' AND prcp > 0.0;
SELECT * FROM weather WHERE city = 'San Francisco' AND prcp > 0.0;

SELECT * FROM weather WHERE city NOT = 'San Francisco' ;
```



### you can request that the results of a query be returned in sorted order:

```jsx title="sql"
\echo

\echo SELECT * FROM weather ORDER BY city;
SELECT * FROM weather ORDER BY city;
--SELECT * FROM weather ORDER BY city DESC;
```

### in this example, the sort order isn't fully specified, 
and so you might get the San Francisco rows in either order. But you'd always get the results shown above if you do
```jsx title="sql"

\echo SELECT * FROM weather ORDER BY city, temp_lo;
SELECT * FROM weather ORDER BY city desc, temp_lo desc;


\echo SELECT * FROM weather ORDER BY city desc, temp_lo desc;
SELECT * FROM weather ORDER BY city desc, temp_lo desc;
```

### you can request that duplicate rows be removed from the result of a query
```jsx title="sql"
\echo
\echo SELECT DISTINCT city FROM weather;
SELECT DISTINCT city FROM weather;


\echo using NOT

\echo SELECT * FROM weather WHERE city NOT IN ('San Francisco', 'New York');
SELECT * FROM weather WHERE city NOT IN ('San Francisco', 'New York');
```
## joins between tables
```jsx title="sql"
\echo SELECT * FROM weather;
SELECT * FROM weather;

\echo SELECT * FROM cities;
SELECT * FROM cities;

```
### inner join
return all the weather records <br/>
together with the location of the associated city<br/>

```jsx title="sql"
\both of these queries will produce same results
\ 'join' is same as 'inner joinseek'
\echo
\echo SELECT * FROM weather JOIN cities ON city = name;
SELECT * FROM weather JOIN cities ON city = name;

\echo
\echo SELECT * FROM weather INNER JOIN cities ON city = name;
SELECT * FROM weather INNER JOIN cities ON city = name;

```
