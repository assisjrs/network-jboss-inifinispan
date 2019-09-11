FROM centos
#VOLUME ~/volume/deployment

USER root

#java 8
RUN yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk/

COPY start.sh /opt/loader/
RUN chmod +x /opt/loader/start.sh

COPY ./target/loader*.jar /opt/loader/loader.jar

ENTRYPOINT /opt/loader/start.sh
