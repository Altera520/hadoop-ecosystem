FROM centos:8

# install dev tools
RUN yum update -y && yum install wget openssh-clients openssh-askpass -y

# passwordless ssh
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN chmod 0600 ~/.ssh/authorized_keys

# java
RUN yum install java-11-openjdk-devel.aarch64 -y

# java env
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:$JAVA_HOME/aarch64_bin

RUN rm -rf /usr/bin/java
RUN ln -s $JAVA_HOME/bin/java /usr/bin/java

# hadoop
RUN wget https://downloads.apache.org/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
RUN tar -xvzf hadoop-3.3.0.tar.gz -C /usr/local
RUN cd /usr/local && ln -s ./hadoop-3.3.0 hadoop
RUN rm hadoop-3.3.0.tar.gz


# hadoop env
ENV HADOOP_HOME /usr/local/hadoop
ENV HADOOP_PREFIX $HADOOP_HOME
ENV HADOOP_COMMON_HOME $HADOOP_HOME
ENV HADOOP_HDFS_HOME $HADOOP_HOME
ENV HADOOP_MAPRED_HOME $HADOOP_HOME
ENV HADOOP_YARN_HOME $HADOOP_HOME
ENV HADOOP_CONF_DIR $HADOOP_HOME/etc/hadoop
ENV YARN_CONF_DIR $HADOOP_HOME/etc/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

# add core-site.xml
ADD core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml