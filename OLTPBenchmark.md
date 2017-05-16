### Installation

Follow these steps to install `oltpbenchmark` suite.

	## Clone our customized oltpbench Git Repository
	git clone https://github.com/oltpbenchmark/oltpbench.git
	
	## Compile OLTP-Benchmark using the provided Ant script
	ant


### Running the Benchmark

**Important:** Peloton uses the Postgres driver. That means you can use any of the existing Postgres sample configuration files. But you must change the `dbtype` to "peloton" in the configuration file.

Before running any benchmark clients, ensure that you have started the Peloton server. You can start the server, as described [here](https://github.com/cmu-db/peloton/wiki/Terminal#start-the-peloton-server).

The following command first loads the ycsb database (`create=true` `load=true`), and then runs the workload described in the `config/peloton_ycsb_config.xml` file. The results (latency, throughput) are summarized into 5 second buckets (-s 5), and the output is written into two files: `outputfile.res` (aggregated) and `outputfile.raw` (detailed).

	## Run the benchmark on Peloton
	./oltpbenchmark -b ycsb 
	-c config/peloton_ycsb_config.xml 
	--create=true --load=true --execute=true 
	-s 5 
	-o outputfile

## Helper shell script    

Here is a [shell script](https://github.com/cmu-db/peloton/blob/master/script/oltpbenchmark/bootstrap_peloton.sh) that you can use to bootstrap peloton and run `YCSB` benchmark.

With this bootstrap script, you need to modify `config/peloton_ycsb_config.xml` with the same default account:

    <username>postgres</username>
    <password>postgres</password>