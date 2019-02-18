# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.


  config.vm.box = "ubuntu/trusty64"

  config.ssh.forward_x11 = true
  config.ssh.forward_agent = true

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.

   config.vm.provision "shell", inline: <<-SHELL

      # Set up basics
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

      # You can use this command to find java home location ( should be /usr/lib/jvm/java-8-oracle/jre/ )
      readlink -f /usr/bin/java | sed "s:bin/java::"

      # Set JAVA_HOME Variable
      echo '\n\n JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"' >> /etc/environment
      source /etc/environment

      # Install Hadoop
      wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.9.0/hadoop-2.9.0.tar.gz
      tar xzf hadoop-2.9.0.tar.gz
      mv hadoop-2.9.0 /usr/local/hadoop
      chmod -R 777 /usr/local/hadoop

      # Set JAVA_HOME Variable in Hadoop
      echo '\n\n export JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"' >> /usr/local/hadoop/etc/hadoop/hadoop-env.sh

      #### Install Pig

      wget http://www-eu.apache.org/dist/pig/pig-0.17.0/pig-0.17.0.tar.gz
      tar -xvf pig-0.17.0.tar.gz
      mkdir /usr/lib/pig
      mv pig-0.17.0 /usr/lib/pig/
      echo '\n\n export PIG_HOME="/usr/lib/pig/pig-0.17.0"' >> /home/vagrant/.bashrc
      echo '\n\n export PATH=$PATH:$PIG_HOME/bin' >> /home/vagrant/.bashrc

      #### Install Hive

      wget http://www-eu.apache.org/dist/hive/hive-2.3.3/apache-hive-2.3.3-bin.tar.gz
      tar -xvf apache-hive-2.3.3-bin.tar.gz
      mkdir /usr/lib/hive
      mv apache-hive-2.3.3-bin /usr/lib/hive/
      echo '\n\n export HIVE_HOME="/usr/lib/hive/apache-hive-2.3.3-bin"' >> /home/vagrant/.bashrc
      echo '\n\n export PATH=$PATH:$HIVE_HOME/bin' >> /home/vagrant/.bashrc      
      echo '\n\n export HADOOP_HOME="/usr/local/hadoop"' >> /usr/lib/hive/apache-hive-2.3.3-bin/bin/hive-config.sh

      ### Install mrjob (mapreduce python library)

      pip install markdown
      pip install testresources
      pip install mrjob --ignore-installed six

   SHELL


end
