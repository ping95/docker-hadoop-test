FROM   centos:7
RUN    yum update
RUN    yum install -y wget vim openssh-server openssh-clients openssh-askpass java-1.8.0-openjdk-devel.x86_64


RUN    ssh-keygen -t rsa -P '' -f ~/.ssh/id_dsa
RUN    cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
RUN    ssh-keygen -f /etc/ssh/ssh_host_rsa_key -t rsa -N ""
RUN    ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -t ecdsa -N ""
RUN    ssh-keygen -f /etc/ssh/ssh_host_ed25519_key -t ed25519 -N "" 

RUN    mkdir /hadoop_home
RUN    cd /hadoop_home
RUN    wget https://archive.apache.org/dist/hadoop/common/hadoop-2.7.7/hadoop-2.7.7.tar.gz
RUN    tar -xvzf hadoop-2.7.7.tar.gz

RUN    java_path_temp=`readlink -f /usr/bin/javac`
RUN    echo export JAVA_HOME=${java_path_temp:0:-10} >> vim ~/.bashrc
RUN    echo export HADOOP_HOME=/hadoop_home/hadoop-2.7.7 >> vim ~/.bashrc
RUN    echo export HADOOP_CONFIG_HOME=$HADOOP_HOME/etc/hadoop >> vim ~/.bashrc
RUN    echo export PATH=$PATH:$HADOOP_HOME/bin >> vim ~/.bashrc
RUN    echo export PATH=$PATH:$HADOOP_HOME/sbin >> vim ~/.bashrc
RUN    echo /usr/sbin/sshd >> vim ~/.bashrc

COPY   ./xml/*.xml  /hadoop_home/hadoop-2.7.7/etc/hadoop
RUN    hadoop namenode -format