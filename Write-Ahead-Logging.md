# Write Ahead Logging
## Accomplished Goals

+ Multi-thread logging and recovery for concurrent txns
+ Single-thread checkpoint creation and recovery
+ Lightweight logging during transaction execution, only log committing txns
+ Cooperate log recovery and checkpoint recovery 
+ Truncate/minimize log files by checkpoint

## Logging Module Design

<img width="700" alt="screen shot 2016-05-06 at 12 30 40 am" src="https://cloud.githubusercontent.com/assets/5545640/15064410/f2f4eda4-1321-11e6-95ce-4b6e383d89d4.png">


Logging manager controls all backend loggers and frontend loggers. It provides interfaces to query and manage these loggers. During Peloton startup, logging manager reads configuration file for log settings. Such as which logging protocol should be used.

The backend loggers are thread-local instances. It is responsible of collecting all logs generated in the work thread.

The frontend logger is a global singleton instance. Logging manager ensures all newly created backend loggers are linked to the frontend loggers. Then the frontend logger continuously collects logs from all registered backend loggers and flush log records to log file or other persistent store.

## Logging Module Workflow and Important Interfaces

<img width="940" alt="screen shot 2016-05-05 at 8 30 17 pm" src="https://cloud.githubusercontent.com/assets/5545640/15061183/3d0a1206-1300-11e6-8248-a8530ed91f42.png">

## Recovery Protocol  
1. **Recover Checkpoint** 
2. **Find min PCID of logs**
3. **Recover transactions in log between Checkpoint id and persistent commit id**
4. **Rebuild Indexes**

## Logging State Diagram

0. **invalid**
1. **Standby** -- Bootstrap
2. **Recovery** -- Optional recovery
3. **Logging** -- Collect data and flush when commit
4. **Terminate** -- Collect any remaining data and flush
5. **Sleep** -- Disconnect backend loggers and frontend logger from manager

![Logging states](https://github.com/cmu-db/peloton/wiki/images/logging_sm.png)

# Write Behind Logging 

## No tuple data in the log file

Only tuple header information is recorded in logs. We use database ID, table ID and tuple offset to refer tuple data in tuple data storage.

## Write Behind Log

All modifications are directly applied to NVRAM without waiting for logs to be flushed.

We rely on MVCC to ensure consistency. So although the updated data is written to persistent storage immediately, they are not visible before all log items are flushed. When all logs get persisted, DBMS sets the version of the database to make all pending updates visible. 

We control tuple update visibility by using commit bits (insert bit and delete bit). Only after logs flushed, logging thread starts to change commit bits in the tuples.

![Logging commit bits and tuple status](https://github.com/cmu-db/peloton/wiki/images/logging_commit_bits.png)

5 steps transaction workflow when doing WBL:

![Logging WBL](https://github.com/cmu-db/peloton/wiki/images/logging_wbl.png)

Extended logging workflow

![Extended logging workflow](https://github.com/cmu-db/peloton/wiki/images/logging_peloton_callmap.png)

A typical Peloton logging log file structure:

![Peloton log file structure](https://github.com/cmu-db/peloton/wiki/images/logging_log_file_structure.png)

## Recovery

Ensure previous run is not interrupt during changing commit bits. Otherwise, redo changing commit bits.

`last_record = final log item in the log file;`

`If (last_record != flush_done_log) {`

    `return; // recover done`

`} else {`

    `Scan file backward;`

    `Set the file cursor after previous commit marked log.`

    `Start read all logs from the cursor to the end of file.`

    `Re-mark all tuples in these log records.`

`}`

## Configuration Options

In `postgresql.conf`:

    peloton_logging_mode       
           invalid             :  disable logging
           aries               :  enable logging
    peloton_checkpoint_mode    
           invalid             :  disable checkpointing
           normal              :  enable checkpointing


## Unit tests

### Test commands

`cd build/tests`

`./logging_test`

`./checkpoint_test`

### Test cases

writing_logfile: execute transaction and write logs.

recovery: turn off logging and write more dummy records. Then reset database and recovery.

### Test options

   -h --help              :  Print help message 

   -t --tuple-count       :  Tuple count.

   -b --backend-count     :  Backend count. Only work for execute transaction.

   -c --check-tuple-count :  Check tuple count. Turn off when test performance.

   -r --redo-all-logs     :  Force redo all logs. Execute transaction will fail because commit is not done

   -d --dir              :  log file dir.