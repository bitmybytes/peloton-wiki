# Introduction

Peloton's interactive terminal allows you to interactively enter, edit, and execute SQL commands. It is very similar to the `psql` program in Postgres. 

# Start Peloton

Launch the peloton binary (which should be accessible on your PATH)    
```
peloton
```
You could also launch Peloton on a custom port as follows

```
peloton -port 5432
```

# Access using PSQL

PSQL is the standard PostgreSQL client. Peloton has been tested to work with psql version 9.5.4.

To connect PSQL to Peloton as the user "postgres", run

```
psql "sslmode=disable" -U postgres
```

If Peloton is running on non-default host or port, run

```
psql "sslmode=disable" -U postgres -h <peloton_host> -p <peloton_port>
```

The latest versions of PSQL clients use SSL encryption to communicate with Postgres servers. It is necessary to disable this feature as Peloton doesn't support SSL-encypted communication yet.

Once PSQL connects successfully you will observe this familiar SQL client interface.

``` 
psql (9.5devel)
Type "help" for help.


postgres=# create table foo(id integer, year integer);
create table foo(id integer, year integer) 0

postgres=# insert into foo values(5, 400);
insert into foo values(5, 400) 1

postgres=# select * from foo;
 id | year 
----+------
  5 |  400
(1 row)
```

# Load in a SQL script and run it using psql

```
psql (9.5devel)
Type "help" for help.

postgres=# \i ../scripts/testing/join/nested_loop_join.sql 
```

# More info on the terminal

[PSQL manual](http://www.postgresql.org/docs/9.5/static/app-psql.html)  
[PSQL common usage](http://postgresguide.com/utilities/psql.html)
