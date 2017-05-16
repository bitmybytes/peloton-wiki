
                                                                                                                         ### Valgrind

Valgrind is useful to find memory problems in Peloton.  

	## Try to use with something like the attached.  
	valgrind --suppress
	valgrind \
    --suppressions=$PG_SOURCE/src/tools/valgrind.supp \
    --trace-children=yes --track-origins=yes --read-var-info=yes \
    peloton -D REST_OF_ARGS

        ## Callgrind
        valgrind --tool=callgrind --trace-children=yes ./src/peloton -D data &> /dev/null &

###  Profiling with Perf

The `Linux kernel` comes with a `performance analysis tool` called perf that can even be used on production servers to `analyze the call stack` of a server, or a process. This is useful to `find the bottlenecks` of a query processing or simply of a server running and improve those.

It is usually found in the `package "perf"`, at least it is the case of RHEL, CentOS and ArchLinux.

/proc/sys/kernel/perf_event_paranoid can be used to restrict access to the performance counters.

     2, allow only user-space measurements
     1, allow both kernel and user measurements (default)
     0, allow access to CPU-specific data
    -1, no paranoid at all


Record information

	## Profile system as long as needed, can be cancelled with Ctrl-C  
	perf record -a -g

	## Profile system for a given period of time  
	perf record -a -g -s sleep $TIME_IN_SECONDS

	## For the duration of a command  
	perf record -a -g -s -- $COMMAND

Different things can be recorded:

    -a to profile the whole system
    -p $PID to profile only the given PID
    -u $USER to profile only the given user

Reports are saved by default in $HOME/perf.data. Old reports are renamed as $HOME/perf.data.old.

	## Real-time measurement is done by perf top, like system-wide profiling  
	perf top

	## Profiling without accumulating stats
	perf top -z

 Viewing the records
   
	## View profile recorded
	perf report -n

	## With a graph
	perf report -g


### Debugging with Strace


	## Run peloton under strace
	strace -o trace.server -f -t peloton -D /path/to/data

	## Run psql under strace
	strace -o trace.client -f -t psql postgres

The first flag is `-f`, which tells strace to follow the forked processes. The `-o` flag sends all the output to a file. We can also use the `-ff` flag, that sends the output corresponding to each forked process to a separate file. Very handy, that. Finally, we add a `-t` flag, which prepends each line with a timestamp.
