FROM jboss/wildfly:9.0.2.Final

#ENV JBOSS_HOME: /opt/jboss/wildfly
#ENV JAVA: /usr/lib/jvm/java/bin/java
#ENV JAVA_OPTS:  -server -XX:+UseCompressedOops  -server -XX:+UseCompressedOops -Xms64m -Xmx512m -XX:MaxPermSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=org.jboss.byteman -Djava.awt.headless=true

EXPOSE 8080
EXPOSE 9990
EXPOSE 8787

#VOLUME ~/volume/deployment

USER root

COPY start.sh /opt/jboss/
RUN chmod +x /opt/jboss/start.sh

RUN yum install -y httpd mod_ssl nmap

COPY 000-default.conf /etc/httpd/conf.d/

RUN systemctl enable httpd

# adds a management user with the following credentials: admin:admin
# if you want to add an application user, use the '-a' option
RUN $JBOSS_HOME/bin/add-user.sh admin admin --silent

RUN chmod +x $JBOSS_HOME/bin/standalone.sh

# cleanup
RUN rm -rf $JBOSS_HOME/standalone/configuration/standalone_xml_history

# cleanup
RUN rm -rf $JBOSS_HOME/standalone/configuration/standalone_xml_history

# automatically launch the standalone configuration
#CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone.xml"]

ENTRYPOINT /opt/jboss/start.sh
