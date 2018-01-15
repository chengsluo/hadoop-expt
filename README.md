# Experiments with Hadoop cluster setups in Docker

This repository provides docker configurations for quick Hadoop cluster
setup.

## Basic Cluster

Provides a 1 `Namenode` and 2 `Datanode` setup.

How to use:

```shell
$ git clone https://github.com/chengsluo/hadoop-expt.git
$ cd hadoop-expt
$ docker-compose -f hadoop-basic.yml up
```

Refer this blog post for more details: http://codito.in/hadoop-cluster-in-docker.

## Credits

Many thanks to [uhopper](https://bitbucket.org/uhopper/hadoop-docker) for
providing excellent base hadoop images.

## Word Count Test

Enter the running namenode container

```shell
$ docker exec -it namenode bash
```

Switch to the mount volume directory

```shell
$ cd /hadoop-data
```

Create the a project directory in hadoop file system

```shell
$ hadoop fs -mkdir -p hdfs://namenode:8020/project/wordcount
```

Upload the need data to hadoop file system

```shell
$ hadoop fs -cp marktwain.txt hdfs://namenode:8020/project/wordcount/marktwain.txt
```

Run the wordCount Application downloaded  from official website

```shell
$ hadoop jar hadoop-mapreduce-examples-2.8.3.jar wordcount hdfs://namenode:8020/project/wordcount hdfs://namenode:8020/project/wordcount/result
```

Pull the result from hadoop file system

```shell
$ hadoop fs -get /project/wordcount/result
```

You can check the result by any text-editor in your local file system now !

```shell
$ cat result/part-r-00000
```



## Version

Hadoop: 2.8.1/2.8.3

Java: 1.8