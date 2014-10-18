FROM qburstdevops/base

MAINTAINER QBurst

ENV KAFKA_HOME /opt/kafka_2.9.2-0.8.1.1
RUN apt-get update
RUN wget -q -N http://project-rt.s3-website-us-east-1.amazonaws.com/softwares/kafka_2.8.0-0.8.1.1.tgz; tar xfz kafka_2.9.2-0.8.1.1.tgz -C /opt; rm kafka_2.9.2-0.8.1.1.tgz

ADD start-kafka.sh /usr/bin/start-kafka.sh 

RUN echo [supervisord] | tee -a /etc/supervisor/supervisord.conf ; echo nodaemon=true | tee -a /etc/supervisor/supervisord.conf

VOLUME ["/var/kafka"]

EXPOSE 9092

ENTRYPOINT ["/usr/bin/start-kafka.sh"]
CMD []
