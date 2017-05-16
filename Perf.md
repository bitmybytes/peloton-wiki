## Profiling with Perf

The kernel comes with a performance analysis tool called [perf](https://perf.wiki.kernel.org/index.php/Tutorial) that can be used to find the performance bottlenecks of a program.

## Installation

       sudo apt-get install linux-tools-generic

## Record information

	## Profile system as long as needed, can be cancelled with Ctrl-C  
	perf record -a -g

	## Profile system for a given period of time  
	perf record -a -g -s sleep $TIME_IN_SECONDS

	## For the duration of a command  
	perf record -a -g -s -- $COMMAND

## Different things can be recorded:

    -a to profile the whole system
    -p $PID to profile only the given PID
    -u $USER to profile only the given user

Reports are saved by default in $HOME/perf.data. Old reports are renamed as $HOME/perf.data.old.

## Viewing the records
   
	## View profile recorded
	perf report -n

	## With a graph
	perf report -g

## Other use cases

	## Real-time measurement is done by perf top, like system-wide profiling  
	perf top

	## Profiling without accumulating stats
	perf top -z

## Perf Configuration

Use this file `/proc/sys/kernel/perf_event_paranoid` to restrict access to the performance counters.

     2, allow only user-space measurements
     1, allow both kernel and user measurements (default)
     0, allow access to CPU-specific data
    -1, no paranoid at all
