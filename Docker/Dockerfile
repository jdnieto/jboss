FROM fedora


ENV JBOSS_HOME /usr/share/wildfly


RUN yum -y install java-1.7.0-openjdk-devel 
RUN yum clean all

RUN cd /usr/share && curl http://download.jboss.org/wildfly/8.1.0.Final/wildfly-8.1.0.Final.tar.gz | tar xz

RUN mv /usr/share/wildfly-8.1.0.Final $JBOSS_HOME

RUN groupadd -r jboss -g 480 && useradd -u 400 -r -g jboss -d $JBOSS_HOME -s /sbin/nologin jboss 

COPY  multi.war $JBOSS_HOME/standalone/deployments/multi.war

RUN chown -R jboss.jboss $JBOSS_HOME/*

EXPOSE 8080 8443 9990 9999

USER jboss
RUN $JBOSS_HOME/bin/add-user.sh admin jboss-123 --silent

cmd ["/usr/share/wildfly/bin/standalone.sh", "-Djboss.bind.address=0.0.0.0", "-Djboss.bind.address.management=0.0.0.0"]
