FROM qburstdevops/base 
MAINTAINER QBurst 

RUN apt-get update 

RUN wget -q -O - http://archive-primary.cloudera.com/cdh5/ubuntu/precise/amd64/cdh/pool/contrib/z/zookeeper/zookeeper_3.4.5+cdh5.1.2+31.orig.tar.gz | tar -xzf - -C /opt
RUN mv /opt/zookeeper-3.4.5-cdh5.1.2/conf/zoo_sample.cfg /opt/zookeeper-3.4.5-cdh5.1.2/conf/zoo.cfg

ENV ZK_HOME /opt/zookeeper-3.4.5-cdh5.1.2
ADD start-zookeeper.sh /usr/bin/start-zookeeper.sh 

RUN ln -s /opt/zookeeper-3.4.5-cdh5.1.2/bin/zkEnv.sh /usr/bin/zkEnv.sh; ln -s /opt/zookeeper-3.4.5-cdh5.1.2/bin/zkServer.sh /usr/bin/zkServer.sh

RUN echo autopurge.purgeInterval=24 | tee -a /opt/zookeeper-3.4.5-cdh5.1.2/conf/zoo.cfg; echo autopurge.snapRetainCount=5 | tee -a /opt/zookeeper-3.4.5-cdh5.1.2/conf/zoo.cfg
RUN echo [supervisord] | tee -a /etc/supervisor/supervisord.conf ; echo nodaemon=true | tee -a /etc/supervisor/supervisord.conf

# (client leader leader.eletion)
EXPOSE 2181 2888 3888

ENTRYPOINT ["/usr/bin/start-zookeeper.sh"]
CMD []
