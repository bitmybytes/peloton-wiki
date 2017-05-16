## Strace

[Strace](http://linux.die.net/man/1/strace) is a linux tool for tracing system calls and signals. 

	## Run peloton under strace
	strace -o trace.server -f -t peloton -D /path/to/data

	## Run psql under strace
	strace -o trace.client -f -t psql postgres

The first flag is `-f`, which tells strace to follow the forked processes. The `-o` flag sends all the output to a file. We can also use the `-ff` flag, that sends the output corresponding to each forked process to a separate file. Very handy, that. Finally, we add a `-t` flag, which prepends each line with a timestamp.
