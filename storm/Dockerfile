FROM qburstdevops/base

MAINTAINER QBurst

RUN wget -q -O - http://project-rt.s3-website-us-east-1.amazonaws.com/softwares/apache-storm-0.9.1-incubating.tar.gz | tar -xzf - -C /opt
ENV STORM_HOME /opt/apache-storm-0.9.1-incubating

RUN apt-get update 

ADD storm.yaml $STORM_HOME/conf/storm.yaml
ADD cluster.xml $STORM_HOME/logback/cluster.xml
ADD start-storm.sh /usr/bin/start-storm.sh 

RUN groupadd storm; useradd --gid storm --home-dir /home/storm --create-home --shell /bin/bash storm; mkdir /var/log/storm; chown -R storm:storm /var/log/storm; ln -s /usr/share/apache-storm-0.9.2-incubating /usr/share/storm; ln -s /usr/share/apache-storm-0.9.2-incubating/bin/storm /usr/bin/storm

RUN echo [supervisord] | tee -a /etc/supervisor/supervisord.conf ; echo nodaemon=true | tee -a /etc/supervisor/supervisord.conf

# nimbus (thrift drpc drpc.invocations)
EXPOSE 6627 3772 3773
# supervisor (slot logviewer)
EXPOSE 6700 8000
# ui
EXPOSE 8080

ENTRYPOINT ["/usr/bin/start-storm.sh"]
CMD []
