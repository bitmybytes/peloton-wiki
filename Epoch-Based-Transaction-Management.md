Peloton can support highly scalable transaction processing on modern multi-core architectures. It implements an epoch-based transaction management scheme for avoiding redundant centralized contention points, where a DBMS thread has to race for shared resources with other threads. A DBMS can confront (at least) three contention points during transaction processing: 

1. timestamp acquisition, where each worker thread acquires a timestamp for its corresponding transaction;

2. garbage collection, where each GC thread checks the progress of each worker thread for detecting expired versions;

3. logging, where each logger thread persists logs into secondary storage.
