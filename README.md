S&P Project

Authors:


======================================================================
Introduction
======================================================================
This README briefly describes the steps involved in this Fred and S&P index project. 


======================================================================
STEP 0: Preliminaries:
======================================================================
Install the following libraries:
    mvn (used to build spark-ts)
    spark-ts
    hbase
    quandl (python library)
    statsmodels (python library)


Setup the following variables in shell
$ export SPARK_HOME="/usr/local/Cellar/apache-spark/2.0.0/libexec/"
$ export PATH=/PATH/TO/SPARK-TIMESERIES/spark-ts/apache-maven-3.3.9/bin:$PATH

Launch pyspark with spark-ts library:
$ cd /Users/sundeepblue/spark-ts/spark-timeseries-master/
$ spark-shell --jars target/sparkts-0.4.0-SNAPSHOT-jar-with-dependencies.jar
$ pyspark --jars target/sparkts-0.4.0-SNAPSHOT-jar-with-dependencies.jar

Launch HBase daemons:
$ cd /usr/local/Cellar/hbase/1.1.5_1/libexec/bin
$ start-hbase.sh
$ hbase thrift start
$ jps

Launch HBase shell
$ cd /usr/local/Cellar/hbase/1.1.5_1/libexec/
$ ./bin/hbase shell

Inside the HBase shell console
> list  # list all tables in HBase
> scan 'Table_YAHOO_INDEX_GSPC'
> list

======================================================================
STEP 1: Fetch FRED time series and S&P index data via Quandl API
======================================================================

See file: “./1__fred_fetch_timeseries_via_quandl_api.html"


======================================================================
STEP 2: Populate all downloaded time series into local HBase
======================================================================

See file: “./2__fred_create_and_populate_hbase_table.html"

======================================================================
STEP 3: Load S&P index from HBase
======================================================================

See file: “./4__fred_sp_index_analysis_using_statsmodels.html"


======================================================================
STEP 4: Perform S&P index analysis using spark-ts (not working)
======================================================================

See file: “./3__fred_sparkts_experiment.html"


======================================================================
STEP 5: Fit seasonal ARIMA model to forecast S&P index via python 'statsmodels' library
======================================================================

See file: “./4__fred_sp_index_analysis_using_statsmodels.html"


======================================================================
Note
======================================================================
It turned out that spark-ts library is still a young library. I did not find quite useful 
documents regarding how to play with it in python. The example that spark-ts provided
(https://github.com/sryza/spark-ts-examples/blob/master/python/Stocks.py) was not working 
on my machine, potentially due to a bug in 'BusinessDayFrequency' class. So I turned
to a python library called 'statsmodels' to fit ARIMA model to forecast S&P index.


