GridDB connector for YCSB

## Overview

GridDB connector for YCSB is a connector that allows execution of [YCSB (Yahoo! Cloud Serving Benchmark)](https://github.com/brianfrankcooper/YCSB/wiki) workloads against GridDB for benchmarking purposes.

## Operating environment

Library building and program execution have been checked in the following environment.

    OS:         CentOS 6.7(x64)
    Java:       JDK 1.7.0_79
    YCSB:       YCSB 0.10.0

## QuickStart

### Preparations

1. Install YCSB

    '$ curl -O --location https://github.com/brianfrankcooper/YCSB/releases/download/0.10.0/ycsb-0.10.0.tar.gz'  
    '$ tar xfvz ycsb-0.10.0.tar.gz'  
    '$ cd ycsb-0.10.0'

    Please refer to https://github.com/brianfrankcooper/YCSB/wiki/Getting-Started.

2. Copy GridDB connector for YCSB under YCSB top directory.

    build.xml  
    griddb/

3. Please edit bin/ycsb as follow.

    DATABASES = {  
        "griddb"       : "com.yahoo.ycsb.db.GridDBClient",  
        ...

4. Build a GridDB Java client and place the created gridstore.jar under the following directory.

    griddb-binding/lib

### Build

Run the following command,   

    $ ant griddb  
    
and create the following jar files.  

    griddb-binding/lib/griddb-binding.jar

### GridDB Setup

Please set the number of cpu core as /dataStore/concurrency in gs_node.json and "32KB" as /dataStore/storeBlockSize in gs_cluster.json.

### Running YCSB

GridDB needs to be started in advance.  
Please execute our program with fieldcount=10 and fieldlength=100 as follows:  

    $ ./bin/ycsb load griddb -P workloads/workloada 
    -p notificationAddress=<GridDB notification address(default is 239.0.0.1)>
    -p notificationPort=<GridDB notification port(default is 31999)>
    -p clusterName=<GridDB cluster name>
    -p userName=<GridDB user name>
    -p password=<GridDB password>
    -p fieldcount=10
    -p fieldlength=100
    $ ./bin/ycsb run griddb -P workloads/workloada 
    -p notificationAddress=<GridDB notification address(default is 239.0.0.1)>
    -p notificationPort=<GridDB notification port(default is 31999)>
    -p clusterName=<GridDB cluster name>
    -p userName=<GridDB user name>
    -p password=<GridDB password>
    -p fieldcount=10
    -p fieldlength=100

## Community

  * Issues  
    Use the GitHub issue function if you have any requests, questions, or bug reports. 
  * PullRequest  
    Use the GitHub pull request function if you want to contribute code.
    You'll need to agree GridDB Contributor License Agreement(CLA_rev1.1.pdf).
    By using the GitHub pull request function, you shall be deemed to have agreed to GridDB Contributor License Agreement.

## License
  
The GridDB connector source license is Apache License, version 2.0.
