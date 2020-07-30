# 综述

每个Spark应用有一个driver程序，用于运行用户的`main`函数、在集群上执行各种各样的并行操作。Spark提供的主要抽象是`resilient distributed dataset(RDD)`，
RDD是一个可分区的、跨集群节点的、可并行操作的元素集合。RDD可通过Hadoop文件系统(或者任何Hadoop支持的文件系统)创建，或者被driver程序中已存在的Scala集合创
建，并且改变它。用户也可以使用Spark持久化一个RDD到内存中，使它在并行操作中被高效的重复使用。RDDs可以自动从失败节点恢复

共享变量是Spark的第二个抽象，可用于并行操作。默认情况下，当Spark在不同节点上作为一组任务并行运行一个函数时，它将函数中使用的每个变量的副本发送给每个任务。
有时，一个变量需要跨任务共享，或者在任务和driver之间共享。Spark支持两种共享变量：broadcast variables，可用于在所有节点的内存中缓存一个值；accumulators:
一个只能"added"的变量，例如计数和求和

# Resilient Distributed Datasets (RDDs)

Spark以RDD为中心，可在并行环境容错的元素集合。有两种创建方式：在driver程序中parallelizing现有集合，