Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/trusty64"
  config.ssh.forward_x11 = true
  config.ssh.forward_agent = true

   config.vm.provision "shell", inline: <<-SHELL

      # Install some basics
      apt-get update
      apt-get install -y apache2
      apt-get install -y -q git wget curl build-essential python python-dev python-setuptools python-pip
      pip install --upgrade pip
      pip install --upgrade virtualenv

      # Install Java 8
      apt-get install -y python-software-properties
      add-apt-repository ppa:webupd8team/java
      apt-get -y -q update
      echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
      apt-get -y install oracle-java8-installer
      update-java-alternatives -s java-8-oracle
      echo '\n\n JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"' >> /etc/environment
      source /etc/environment

      # Install Hadoop
      wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.9.0/hadoop-2.9.0.tar.gz
      tar xzf hadoop-2.9.0.tar.gz
      mv hadoop-2.9.0 /usr/local/hadoop
      chmod -R 777 /usr/local/hadoop
      echo '\n\n export HADOOP_HOME="/usr/local/hadoop/"' >> /home/vagrant/.bashrc
      echo '\n\n export PATH=$PATH:$HADOOP_HOME/bin' >> /home/vagrant/.bashrc
      echo '\n\n export JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"' >> /usr/local/hadoop/etc/hadoop/hadoop-env.sh

      # Install Pig
      wget http://www-eu.apache.org/dist/pig/pig-0.17.0/pig-0.17.0.tar.gz
      tar -xvf pig-0.17.0.tar.gz
      mkdir /usr/lib/pig
      mv pig-0.17.0 /usr/lib/pig/
      echo '\n\n export PIG_HOME="/usr/lib/pig/pig-0.17.0"' >> /home/vagrant/.bashrc
      echo '\n\n export PATH=$PATH:$PIG_HOME/bin' >> /home/vagrant/.bashrc

      # Install Hive
      wget http://www-eu.apache.org/dist/hive/hive-2.3.4/apache-hive-2.3.4-bin.tar.gz
      tar -xvf apache-hive-2.3.4-bin.tar.gz
      mkdir /usr/lib/hive
      mv apache-hive-2.3.4-bin /usr/lib/hive/
      echo '\n\n export HIVE_HOME="/usr/lib/hive/apache-hive-2.3.4-bin"' >> /home/vagrant/.bashrc
      echo '\n\n export PATH=$PATH:$HIVE_HOME/bin' >> /home/vagrant/.bashrc      
      echo '\n\n export HADOOP_HOME="/usr/local/hadoop"' >> /usr/lib/hive/apache-hive-2.3.4-bin/bin/hive-config.sh

      # Install mrjob (mapreduce python library)
      pip install markdown
      pip install testresources
      pip install mrjob --ignore-installed six

   SHELL

end