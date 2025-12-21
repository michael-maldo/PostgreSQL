---
sidebar_position: 3
---
# psql meta commands
slash commands

## tips and caveats
### make sure to use \ (back slash) not! / (forward slash) 
``` jsx title="sql"
\meta_command
```

### sql commands ends with semicolon ;
; tells the SQL client  "Execute this SQL statement."
```jsx title="sql"
SELECT * FROM tablename;
```

### set search_path
``` jsx title="sql"
SET SEARCH_PATH TO schema1, schema2;
SHOW SEARCH_PATH;
```
### you can use -- to write comments in sql
```jsx title="sql"
-- this is a comment, everything is treated as comment until end of the line
```

## connection
### show current connection
```jsx title="sql"
\conninfo
```
### connect to a database
```jsx title="sql"
\c dbname
```

## db
### list available databases
```jsx title="sql"
\l
```

## schema
### show available schemas in current db connection
```jsx title="sql"
-- list schemas available in current db
\dn

-- search_path control which schema(s) PostgreSQL looks in first
-- without setting search_path ( defaults to public schema )
SELECT * myschema.mytable ; 

-- when search_path set to myschema
-- no need to specify schema in the query
SELECT * FROM mytable;


-- set search_path
SET SEARCH_PATH TO schema_name1, schema_name2;

-- show current search_path settings
SHOW SEARCH_PATH;
```

## relations
```jsx title="sql"
-- list all relations in a a search path
\d
\dt
\dt+

-- desbcribe all relation's - columns, types
\d schema_name.*
\d schema_name.table_name

-- describe all relations in all schema in current db
\d *.*

-- output can be redirected to a file
\o outfile.txt
-- reset output to psql terminal
\o
```

## psql run sql scripts from a file
### sql script files 
can contain both sql and psql metacommands
#### from the shell
```jsx title="sql"
psql -f scripts.sql
```
#### from inside psql - path settings/searching apply
```jsx title="sql"
\i scripts.sql
```

#### issue command line from inside psql
This executes pwd in the shell, not inside PostgreSQL.
```jsx title='sql'
-- psql internal command to change directory
-- this is useful when using \i, executes sql in a file
\cd

-- executes linux command from inside psql
-- confirms cd has been perfomed
\! pwd

-- check files available in current directory
\! ls
\1 ls -l

```

