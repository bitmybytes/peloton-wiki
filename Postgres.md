
### Published Papers from Original Developers
* [The Design of Postgres] (http://www.postgresql.org.es/sites/default/files/ERL-M85-95.pdf)
* [The Implementation of Postgres] (http://www.postgresql.org.es/sites/default/files/ERL-M90-34.pdf)

### Github Repositories
* Peloton: https://github.com/cmu-db/peloton
* Postgres: https://github.com/cmu-db/postgres

### Documentation
* [PSQL wired protocol] (https://www.postgresql.org/docs/9.1/static/protocol.html)
* Architecture: http://www.postgresql.org/developer/backend/
* Architecture: https://cisc322.files.wordpress.com/2010/09/cisc-322-conceptual-architecture.pdf
* Documentation: http://www.postgresql.org/docs/9.4/static/internals.html
* Eclipse: https://wiki.postgresql.org/wiki/Working_with_Eclipse

### Doxygen
* http://doxygen.postgresql.org/

### Developer FAQ
* https://wiki.postgresql.org/wiki/Developer_FAQ

### Understanding Source Code - Good Starting Point

Function Name : File Name : Line # : Description

* `exec_simple_query`: `src/backend/tcop/postgres.c` L883
  Example of entire query execution

* `standard_ExecutorRun`: `src/backend/executor/execMain.c` L303
  DML/Executor hand-off

* `ProcessUtility`: `src/backend/tcop/utility.c` L325
  DDL/Utility hand-off

### Useful Links
* [A Tour of PostgreSQL Internals] (http://www.postgresql.org/files/developer/tour.pdf)
* [Introduction to Hacking PostgreSQL] (http://www.neilconway.org/talks/hacking/hack_slides.pdf)
* [Explaining EXPLAIN] (https://wiki.postgresql.org/images/4/45/Explaining_EXPLAIN.pdf)
* [Introduction to Hacking PostgreSQL: with lots of Code Review] (https://www.linux.org.au/conf/2007/att_data/Miniconfs%282f%29PostgreSQL/attachments/hacking_intro.pdf)
* [Following a Select Statement Through Postgres Internals] (http://patshaughnessy.net/2014/10/13/following-a-select-statement-through-postgres-internals)
* [Discovering the Computer Science Behind Postgres Indexes] (http://patshaughnessy.net/2014/11/11/discovering-the-computer-science-behind-postgres-indexes)