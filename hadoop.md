# This is hadoop note
Hadoop
    considerationis
        More data usually beats better algorithms
        VIrtual access to information
            HDFS
                Hadoop Distributed Filesystem
                RAID
        Aggregate data
            MapReduce
        seek time improving more slowly than transfer rate
            seek
                Moving the disk's head to a particular place on the disk to read /write
                latency of a disk operation
            transfer rate
                disk's bandwidth
        Update date majority of database MapReduce is faster  
            MapReduce
            relational database
                B-tree
        Comparison
            RDBMS
                low-latency retrieval
                Update times of a small amount of data
                continually updated
                structured data
                normalized
                    retain integrity
                    remove redundancy
                Double input sizes lead to more slower than 2
            MapReduce
                writes once
                read many times
                interpret the data at processin time
                    semi-structured
                    unstructured data
                not normalized
                    makes reading a record nonlocal operation
                Double intput size, double cluster size, same performance
            PIg, Hive make MapReduce works like RDBMS
    function
        kernel
            a reliable shared storage
                HDFS
            analysis system
                MapReduce
        Common
            components
            interfaces
            For distributed filesystems and general I/O
                Serialization
                Java RPC
                Persistent data structures
        Avro
            a serialization system 
            For 
                efficient, cross-language RPC
                Persistent data storage
        MapReduce
            A distributed data processing model
            execution environment
            run on
                large clusters
                commodity machines
            Why MapReduce is better than Parallel processing?
                任务分配不均
                均匀分块后仍然需要按照key合并
                整体表现收到单机性能影响
                    单机performance难以加速
                    集群可靠性、协作性管理
            DataFlow
                Job
                    input data
                    MapReduce program
                    configuration information
                    tasks
                        map tasks
                        reduce tasks
                    trakers
                        jobtracker
                            coordinates all the jobs by scheduling tasks to run on tasktrackers
                            overall progress of each job
                            if a task fails, reschedule it on a different tasktracker
                        tasktrackers
                            run tasks
                            send progress reports to the jobtracker
                    fine-grained splits
                        splits are small to be load balancing
                        too small, overhead of managing and map task creation dominate
                        64M by default
                    data locality optimization
                Streaming
                    ruby
                    python
                Pipes
                    C++
        HDFS
            assumption
                very large files
                    100M ~10TB
                Write once, read-many-times
                various analyses are performed on that dataset
                analysis will involve a large proportion
                read the whole dataset >> the latency in reading the first record
                carry on working without interruption to user
            pitfall
                Low-latency data access
                    <100 ms
                Lots of small files
                    storing files' meta information takes memory
                    Sorting files
                Multiple writers
                    files can be extended only, not insert
            Concepts
                Blocks
                    system level
                        512 bytes
                    hodoop
                        64MB
                            data transfer << seek
                            MapReduce operate on one block at a time
                        Benefits
                            files can be anywhere
                            simplifying the storage system
                                meta data are not with blocks
                            replication
                        hadoop fsck/ -files -blocks
                nodes
                    Namenodes
                        manage file systems
                            filesystem tree
                            metadata for all the files and dir
                        resilient to failure
                            backup meta data
                            secondary namenode
                    Datanodes
                        workhorses
                Federation
                    scale by adding namenodes
                    more files, more blocks
                    each manages a portion of the filesystem namespace
                    eg. A manage /usr, B manage /share
                High-Availability
                    Subtopic 1
        Pig
            a data flow language and execution environment
            for exploring very large datasets
            run on
                MapReduce
                HDFS
        Hive
            a distributed data warehouse
            mange data stored in HDFS
            provides a query language based on SQL
            一种能执行MapReduce作业的类SQL编程接口
        HBase
            database
                A distributed
                column-oriented
            一种非关系型的数据库结构
            supports
                batch-style computations using MapReduce
                point queries(random reads)
        ZooKeeper
            coordination service
                distributed
                highly available
            primitives
                eg
                    distributed locks
                    for building distributed applications
        Sqoop
            bulk transfers tool
                HDFS
                structured data stores
        Oozie
            running and scheduling workflows of Hadoop jobs
                Pig
                MapReduce
                Hive
                Sqoop
        MapReduce 2, YARN
            Yet Another Resource Negotiator
            Resource Manager for unning distributed applications
