# Lab 3 Hive & Pig

This lab covers material from Week 3 and Week 4 of CA675 (Hive and Pig). 
We will install HIVE and PIG and start practicing with their basic functions separately. 
Both of these applications can either run on top of a working HDFS / Mapreduce cluster, or they can run in local mode (useful for debugging).

## Vagrant file

The Vagrantfile above (upoaded 18/2/19 4:30pm) contains working installation of Java 8, Hadoop, Pig, Hive & mrjob.

Edit (19/2/19 4pm) - VM RAM allocation changed to 2 GB to avoid memory errors with hadoop.

Edit (20/2/19 5pm) - Ubuntu version changed from trusty to xenial. Trusty going out of use in April.

## HIVE

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

## PIG 

1. Install Pig <https://pig.apache.org/docs/r0.15.0/start.html>
(Optionally, install Hadoop / HDFS and Copy the source files to the HDFS)

2. Toy Example:
      - Create two CSV file as follows:
            * A.txt containing two lines: (0,1,2) and (1,3,4)
            * B.txt containing two lines: (0,5,2) and (1,7,8)
      - Run the PIG Latin commands below, one by one from shell, and observe what is contained in d, e, f and g after each dump (note the content of g and reflect upon the way pig handles schema on the fly

```
a = LOAD ‘A.txt’ using PigStorage(‘,’); 
b = LOAD ‘B.txt’ using PigStorage(‘,’); 
c = UNION a,b;
SPLIT c INTO d IF $0==0, e IF $0==1; 
dump d;
dump e;
f = FILTER c BY $1>3;
dump f;
A = LOAD ‘A.txt’ using PigStorage(‘,’) as (a1:int, a2:int, a3:int); 
B = LOAD ‘B.txt’ using PigStorage(‘,’) as (b1:int, b2:int, b3:int); C = UNION A,B;
g = FOREACH c GENERATE a2, a2*a3
dump g;
```

3. Example 1:
      * Create a CSV file named example1.txt containing few entries for (url, category, pagerank)
      * Run the pig commands from lecture slides (Example 1) that allow you to "find, for each sufficiently large category, the average pagerank of high-pagerank urls in that category"

4. Example 2:
      * Create two CSV files named example2users.txt containing (userID, user_age) and example2websites.txt containing (userID,url,timestamp) respectively
      * Run the pig commands from lecture slides (Example 2) to "find the top 5 most visited sites by users aged in the range (18,25)"


## Some extra help installing PIG & HIVE:
 
Download PIG tar file
`wget http://ftp.heanet.ie/mirrors/www.apache.org/dist/pig/pig-0.17.0/pig-0.17.0.tar.gz`
 
Then carry out the follow steps to get it working 
1. Unpack 
2. Move folder 
3. Set PIG_HOME
4. Add to path
Outlined here in detail:
https://archanaschangale.wordpress.com/2013/10/14/pig-installation-on-ubuntu/
(You may not have to cd into downloads & may need to use nano instead of gedit to edit files)

Download HIVE tar file 
`wget http://ftp.heanet.ie/mirrors/www.apache.org/dist/hive/stable-2/apache-hive-2.3.2-bin.tar.gz` 
 
Copy the same procedure as for pig above. (Unpack, move, set HIVE_HOME and add to path)
 
Then set hadoop home variable in hive as per the following: 
https://stackoverflow.com/questions/36044498/issues-with-installing-hive-on-ubuntu-hadoop-home-or-hadoop-prefix-must-be-se
