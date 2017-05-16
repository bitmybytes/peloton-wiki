[![Peloton](http://db.cs.cmu.edu/wordpress/wp-content/uploads/2015/11/peloton.jpg)](http://pelotondb.org/)

**Welcome to the Peloton wiki. Please choose your topic from the sidebar on the right.**

## What Is Peloton?

* Peloton is a self-driving SQL database management system.
* Integrated artificial intelligence components that enable autonomous optimizations.
* Native support for byte-addressable non-volatile memory (NVM) storage technology.
* Lock-free multi-version concurrency control to support real-time analytics.
* Postgres wire-protocol and JDBC compatible.
* High-performance, lock-free Bw-Tree for indexing.
* 100% Open-Source (Apache Software License v2.0).

## What Problem Does Peloton Solve?

In the last two decades, both researchers and vendors have built advisory tools to assist database administrators in various aspects of system tuning and physical design. Most of this previous work, however, is incomplete because they still require humans to make the final decisions about any changes to the database and are reactionary measures that fix problems after they occur.

What is needed for a truly “self-driving” database management system (DBMS) is a new architecture that is designed for autonomous operation. This is different than earlier attempts because all aspects of the system are controlled by an integrated planning component that not only optimizes the system for the current workload, but also predicts future workload trends so that the system can prepare itself accordingly. With this, the DBMS can support all of the previous tuning techniques without requiring a human to determine the right way and proper time to deploy them. It also enables new optimizations that are important for modern high-performance DBMSs, but which are not possible today because the complexity of managing these systems has surpassed the abilities of human experts.

Peloton is a relational database management system designed for fully autonomous optimization of hybrid workloads.
