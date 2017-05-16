This page lists the current status of TPC-H support in Peloton.  For each of the 22 TPC-H queries, we list whether it works, and if not, what the cause of the issue is.

| Query         | Supported     | Cause of error  |
| ------------- |:-------------:|:---------------:|
| [Query #1](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query1.sql)      | &#x2714;      | |
| [Query #2](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query2.sql)      | &#x2714;      | |
| [Query #3](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query3.sql)      | &#x2714;      | |
| [Query #4](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query4.sql)      | &#x2715;      | Lacking support for SEMI joins.|
| [Query #5](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query5.sql)      | &#x2714;      | |
| [Query #6](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query6.sql)      | &#x2714;      | |
| [Query #7](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query7.sql)      | &#x2715;      | Lacking support for subplans as expressions.|
| [Query #8](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query8.sql)      | &#x2715;      | |
| [Query #9](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query9.sql)      | &#x2715;      | |
| [Query #10](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query10.sql)     | &#x2714;      | |
| [Query #11](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query11.sql)     | &#x2714;      | |
| [Query #12](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query12.sql)     | &#x2714;      | |
| [Query #13](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query13.sql)     | &#x2714;      | |
| [Query #14](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query14.sql)     | &#x2715;      | Null error. |
| [Query #15](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query15.sql)     | &#x2715;      | Relies on materialized view.|
| [Query #16](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query16.sql)     | &#x2714;      | |
| [Query #17](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query17.sql)     | &#x2715;      | Lacking support for subplans as expressions.|
| [Query #18](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query18.sql)     | &#x2714;      | |
| [Query #19](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query19.sql)     | &#x2715;      | Unknown.|
| [Query #20](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query20.sql)     | &#x2715;      | Lacking support for subplans as expressions.|
| [Query #21](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query21.sql)     | &#x2715;      | Lacking support for ANTI join. Incorrect mapping from Postgres plan to Peloton plan.|
| [Query #22](https://github.com/oltpbenchmark/oltpbench/blob/master/src/com/oltpbenchmark/benchmarks/tpch/queries/query22.sql)     | &#x2715;      | Lacking support for ANTI join. Incorrect mapping from Postgres plan to Peloton plan.|