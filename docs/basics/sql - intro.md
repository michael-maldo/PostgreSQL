---
sidebar_position: 1
---

# sql - intro
these commands are sequential<br/>
creates db, schema, sets search_path, creates and populates tables<br/>
then follows with queries, joins<br/>


## initialize basicsdb database
```jsx title="psql"
drop database if exists basicsdb; -- if db exists, drop it first

create database basicsdb;
\c basicsdb
```

## add basics schema
```jsx title="psql"
create schema if not exists basics;
set search_path to basics, public;
show search_path;
```

## creating a new table
```jsx title="sql"
drop table if exists weather;
CREATE TABLE if not exists weather (
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
COPY weather from '/var/lib/pgsql/scripts/weather.txt';
SELECT * from weather;
COPY weather TO '/var/lib/pgsql/scripts/weather.copy.txt';


INSERT INTO cities VALUES ( 'San Francisco', '(-122.4194, 37.7794)');
INSERT INTO cities VALUES ( 'New York', '(-74.0060, 40.7128)');

\echo select * from cities;
select * from cities;


\dt basics.*

\d basics.*
```

## querying a table

### select *
\echo select * from weather;
select * from weather;

\echo SELECT city, temp_lo, temp_hi, prcp, cur_date FROM weather;
SELECT city, temp_lo, temp_hi, prcp, cur_date FROM weather;


### you can write expressions
not just simple column references, in the select list.

```agsl
\echo SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, cur_date FROM weather;
\echo

SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, cur_date FROM weather;
```



### a query can be “qualified”
by adding a WHERE clause that specifies which rows are wanted.<br /> 
The WHERE clause contains a Boolean (truth value) expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (AND, OR, and NOT) are allowed in the qualification

```agsl
\echo
\echo SELECT * FROM weather WHERE city = 'San Francisco' AND prcp > 0.0;
SELECT * FROM weather WHERE city = 'San Francisco' AND prcp > 0.0;

SELECT * FROM weather WHERE city NOT = 'San Francisco' ;
```



### You can request that the results of a query be returned in sorted order:

```


\echo

\echo SELECT * FROM weather ORDER BY city;
SELECT * FROM weather ORDER BY city;
--SELECT * FROM weather ORDER BY city DESC;
```

### In this example, the sort order isn't fully specified, 
and so you might get the San Francisco rows in either order. But you'd always get the results shown above if you do
```agsl

\echo SELECT * FROM weather ORDER BY city, temp_lo;
SELECT * FROM weather ORDER BY city desc, temp_lo desc;


\echo SELECT * FROM weather ORDER BY city desc, temp_lo desc;
SELECT * FROM weather ORDER BY city desc, temp_lo desc;
```

### you can request that duplicate rows be removed from the result of a query
```agsl




\echo
\echo SELECT DISTINCT city FROM weather;
SELECT DISTINCT city FROM weather;


\echo using NOT

\echo select * from weather WHERE city NOT IN ('San Francisco', 'New York');
select * from weather WHERE city NOT IN ('San Francisco', 'New York');
```

### joins between yables

```agsl
\echo select * from weather;
select * from weather;

\echo select * from cities;
select * from cities;

```

### return all the weather records 
#### together with the location of the associated city

```agsl
\echo
\echo select * from weather join cities on city = name;
select * from weather join cities on city = name;



\echo
\echo select * from weather inner join cities on city = name;
select * from weather inner join cities on city = name;

```
