## GDB Environment
   
Set up gdb environment by copying these lines into `~\.gdbinit`:

	# We have scroll bars in the year 2015!  
	set pagination off

	# Attach to both parent and child on fork  
	set detach-on-fork off

	# Stop/resume all processes  
	set schedule-multiple on
 
	# Usually don't care about these signals  
	handle SIGUSR1 noprint nostop
	handle SIGUSR2 noprint nostop

	# Ugly hack so we don't break on process exit  
	python gdb.events.exited.connect(lambda x: [gdb.execute('inferior 1'), gdb.post_event(lambda: gdb.execute('continue'))])

## Start Peloton Under GDB

	## Stop peloton server  
	pg_ctl -D ./data stop

	## Launch peloton under gdb  
	gdb --args peloton -D ./data 

## Useful Links

* [Starting Postgres under GDB] (https://wiki.postgresql.org/wiki/Getting_a_stack_trace_of_a_running_PostgreSQL_backend_on_Linux/BSD#Starting_Postgres_under_GDB)
* [Tips and tricks from an open-source developer] (http://michael.otacoo.com/manuals/postgresql/)
* [Compilation of useful links] (https://github.com/ty4z2008/Qix/blob/master/pg.md)
