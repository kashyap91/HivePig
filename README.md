This lab covers material from Week 3 and Week 4 of CA675 (Hive and Pig). 
We will install HIVE and PIG and start practicing with their basic functions separately. 
Both of these applications can either run on top of a working HDFS / Mapreduce cluster, or they can run in local mode (useful for debugging).

# Install Java

# Install Java 8

      `apt-get install -y python-software-properties
      add-apt-repository ppa:webupd8team/java
      apt-get -y -q update
      echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
      apt-get -y install oracle-java8-installer
      update-java-alternatives -s java-8-oracle
      
# Set JAVA_HOME Variable

You can use this command to find java home location ( should be /usr/lib/jvm/java-8-oracle/jre/ )
`readlink -f /usr/bin/java | sed "s:bin/java::"`

Set JAVA_HOME Variable
`echo '\n\n JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"' >> /etc/environment source /etc/environment``

# Install Hadoop

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

# PIG (more on this after week 4 on PIG)

1. Install Pig <https://pig.apache.org/docs/r0.15.0/start.html>
(Optionally, install Hadoop / HDFS and Copy the source files to the HDFS)


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
