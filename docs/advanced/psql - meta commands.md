---
sidebar_position: 1
---
# psql meta commands
# commonly used meta commands
(slash commands)

## tips and caveats
### make sure to use \ (back slash) not! / (forward slash) 
``` agsl
\meta_command
```
### when entering sql commands make sure to end with ; (semicolon)
otherwise the prompt is not executing the sql yet until it sees a ;
```agsl
set search_path to schema1, schema2;
show search_path;
```
### you can use -- to write comments in sql
```agsl
-- this is a comment, everything is treated as comment until end of the line
```

## connection
### show current connection
```agsl
\conninfo
```
### connect to a database
```agsl
\c dbname
```

## db
### list available databases
```agsl
\l
```

## schema
### show available schemas in current db connection
```agsl
-- list schemas available in current db
\dn

-- search_path control which schema(s) PostgreSQL looks in first
-- without setting search_path ( defaults to public schema )
select * myschema.mytable ; 

-- when search_path set to myschema
-- no need to specify schema in the query
select * from mytable;


-- set search_path
set search_path to schema_name1, schema_name2;

-- show current search_path settings
show search_path;
```

## relations
```agsl
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
```agsl
psql -f scripts.sql
```
#### from inside psql - path settings/searching apply
```agsl
\i scripts.sql
```

#### issue command line from inside psql
This executes pwd in the shell, not inside PostgreSQL.
```jsx title='sql'
\! pwd
```

