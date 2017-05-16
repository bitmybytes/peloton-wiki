
We support different kinds of constraints in Peloton now:

####In <code>CREATE TABLE</code> statements:

<code>NOT NULL</code>

Users can set not null constraint to a single column and null value inserted in to that column will be rejected. Example:
> CREATE TABLE mytable (id INTEGER, name VARCHAR(20) NOT NULL);   

 
<code>UNIQUE</code>

We support the unique constraint on a single column or on multi-columns. A non-duplicated Btree index is built on the target column(s) and every insertion, update and deletion will lead to operations in the Btree.
Example: 
> CREATE TABLE mytable (id INTEGER UNIQUE, name VARCHAR(20));  



<code>PRIMARY KEY</code>

A single column or multi-columns can be assigned as the primary key of a table.
Example: 
> CREATE TABLE mytable (id INTEGER PRIMARY KEY, name VARCHAR(20));  



<code>FOREIGN KEY</code>

Foreign key constraint is implemented in Peloton. On delete/update, modes of **NO ACTION**, **RESTRICT**, **SET NULL** and **CASCADE** are supported.
Example:
> CREATE TABLE department (did INTEGER PRIMARY KEY, name VARCHAR(20));

> CREATE TABLE employee (id INTEGER PRIMARY KEY, name VARCHAR(20), department INTEGER REFERENCES deparment(did));



<code>CHECK</code>

Check constraints, involving single column or many columns, are implemented in Peloton.
Example:
> CREATE TABLE c1 ( a integer, b integer, c integer, CHECK (a * b > c + 1) );

> CREATE TABLE c2 ( product_no integer PRIMARY KEY, name text, price numeric, CHECK (price > 10), discounted_price numeric, CONSTRAINT valid_discount CHECK (price > discounted_price AND discounted_price > 0) );


####In <code>ALTER TABLE</code> statements:

<code>SET NOT NULL</code>

We can dynamically add a not null constraint to a column. If a null value already exists in this column, this alter table statement will be rejected.
Example:
> CREATE TABLE t1 ( id INTERGER, name VARCHAR(20) );
> ALTER TABLE t1 ALTER COLUMN name SET NOT NULL;


<code>DROP NOT NULL</code>

A not null constraint can be dropped. Afterwards null values are accepted in this column.
Example:
> CREATE TABLE t1 ( id INTERGER, name VARCHAR(20) NOT NULL);

> ALTER TABLE t1 ALTER COLUMN name DROP NOT NULL;


<code>ADD CONSTRAINT UNIQUE</code>

An unique constraint can be added to one or many columns after this table has been created. When an unique constraint is to be added, we first check if there are duplicated values in the target column(s). If so, this alter table statement will be rejected. Otherwise, a Btree index will be built on the target column(s).
Example:
> CREATE TABLE t1 ( id INTERGER, name VARCHAR(20));

> ALTER TABLE t1 ADD CONSTRAINT myron UNIQUE(name);


              

<code>DROP CONSTRAINT UNIQUE</code>

The unique constraint dynamically added can be dropped later.
Example:
> CREATE TABLE t1 ( id INTERGER, name VARCHAR(20));

> ALTER TABLE t1 ADD CONSTRAINT mycon UNIQUE(name);

> ALTER TABLE t1 DROP CONSTRAINT mycon;