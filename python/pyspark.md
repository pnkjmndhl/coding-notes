### apache spark ecosystem
    - Spark SQL and Dataframes
        - DataFrame programming abstraction
        - complex analytics with SQL
    - Streaming
        - process realtime data
        - analyze streaming and historical data
        - use similar code for batch data and real-time data
    - MLlib
        - provides scalable machine learning
        - works in memory (100x mapreduce)
    - GraphX
        - enables working with graph-structured data at scale
        - include a new graph abstraction, the directed multigraph
        - useful for visualizing social networks
- Spark Core API (scala, java, python, r, sql)
    - contains basic functionality of task scheduling, memory management, fault recovery, interacting with storage systems


### why Spark?
- pandas (good but)
    - tabular data
    - can hundle hundreds of thousands to millions of rows
    - mature and feature rich
    - limited to single machine
- hadoop (good but)
    - was the big data platform
    - compute system and storage system closely integrated
    - HDFS and replication
    - spark can do it in memory; hadoop has to read from and write to disk (100x faster)
- Dask
    - written in python and only supports python
    - part of the python ecosystem
    - doesnot support SQL


### cluster manager types
- standalone
- Apache Mesos
- Hadoop YARN
- Kubernetes

### creaging a SparkSession
- creating a spark session is the first step of any Spark application
- with spark 2.0, a spark session can access all of the sparks's functionality through a single, unifed point of entry

### paritions, transformations, lazy evaluations, and actions
- wait till the last moment -> lazy evaluation
- view data
    - `.show()`
- collect data
    - `.collect()`
- write data
    - `.write.format(...)`