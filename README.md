For this Lab, we will install HIVE and PIG and start practicing with their basic functions separately. 
Both of these applications can either run on top of a working HDFS / Mapreduce cluster, or they can run in local mode.

# HIVE

1. Install Hive (see slides Week 3 and Manual link below)
   <https://cwiki.apache.org/confluence/display/Hive/GettingStarted>
   Some key steps:
   1. Note you will need Java >6 and Hadoop 0.20.x or greater
   1. Set $HADOOP_HOME environment variable (done when you installed hadoop)
   1. Set $HIVE_HOME and add hive to PATH
   1. Bootstrap locations used to store files on HDFS
      - $ hdfs dfs -mkdir /tmp
      - $ hdfs dfs -mkdir /user/hive/warehouse
      - $ hdfs dfs -chmod g+w /tmp
      - $ hdfs dfs -chmod g+w /user/hive/warehouse
   1. Run the shell (of the three modes to run HIVE, we will use command line)
      - $ hive
   

2. Check examples to Create, Load, Query data with Hive (slide 17 onwards)
   * <http://courses.coreservlets.com/Course-Materials/pdf/hadoop/07-Hive-01.pdf>
   
3. Create your own tables and load data from a .txt file you have created or downloaded, then practice some queries.
You can find more query examples and SQL cheat-sheet at the links below
   * https://hortonworks.com/blog/hive-cheat-sheet-for-sql-users/
   * https://support.treasuredata.com/hc/en-us/articles/360001457347-Hive-Query-Language#hive-example-query-catalog

# PIG (come back to this after week 4 on PIG)

1. Install Pig <https://pig.apache.org/docs/r0.15.0/start.html>
(Optionally, install Hadoop / HDFS and Copy the source files to the HDFS)

