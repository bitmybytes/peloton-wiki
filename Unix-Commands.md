## List the peloton processes

	pgrep "peloton" | xargs ps fp
	
## Kill all the peloton processes

	pkill -9 peloton
	
## List all the files ending with .cpp extension

	find . -name "*.cpp" -exec ls {} \;
	
## Replace all foo with bar in all files with that extension

	find . -name "*.cpp" -exec sed -i 's/foo/bar/' {} \;
	
## Quick Setup Script

The shell script `run.sh` is located in `/scripts/oltpbenchmark`.
