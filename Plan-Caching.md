## Plan Caching

Peloton supports prepared statement through plan caching. Currently, user can only make use of prepared statement via connectivity API. `PREPARE` and `EXECUTE` keywords have not been supported yet. To describe how Peloton caches plan, it is necessary to talk about how Postgres implements plan caching. 

There are generally two major paths for Postgres. One-shot query such as a query typed in `psql` without using `PREPARE` command, is called a `simple query`. Such queries are never cached and would be handled by `exec_simple_query()`. However, if the user uses prepared statement feature via, say, JDBC driver, 3 steps need to be done for one instance of a query to be execute completely. 

The first step is `parse`. A prepared statement that leaves parameters blank would first need to be parsed and planned. Whether the plan would be cached is determined by several things. Database connectivity driver implementations have an idea called `client side prepared statement`. A prepared statement would not become a `server side prepared statement` until certain configurable number of invocation is reached. After then, Postgres would start to consider caching the plan. By "start to consider", I mean that even if your database driver is on `server side prepared statement` mode, Postgres will use some heuristics to decide whether or not to cache, such as not caching until 5 invocations. Once a plan is cached, it would be called a `named statement` and be given a name, if the user does not give one. The name is meaningful on a per connection basis. 

The second step is `bind`. In this step, let it be a `named statement` or a `unnamed statement`, Postgres binds parameters to their corresponding plan. To be specific, as users specify parameters in their client code, the database driver stores the parameters at client side first. Once all parameters are given, the database driver would send one message to Postgres with all parameters. And the `bind` step would triggered at server side.

The third step is `execute`. This is triggered by client code and a prepared statement with parameters would be executed.

Peloton make use of the name of the plan as key for plan caching. The value is a shared pointer of type `AbstractPlan`. Least Recently Used or LRU replacement policy is used. Since a cached plan is only meaningful within a connection, no synchronization is needed to manipulate the per-connection plan cache.
