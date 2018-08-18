FROM centos:7

ARG JAVA_RPM_VERSION

USER root

RUN mkdir -p /deployments

# JAVA_APP_DIR is used by run-java.sh for finding the binaries
ENV JAVA_APP_DIR=/deployments \
    JAVA_MAJOR_VERSION=8

# /dev/urandom is used as random source, which is prefectly safe
# according to http://www.2uo.de/myths-about-urandom/
RUN yum install -y \
       java-1.8.0-openjdk-${JAVA_RPM_VERSION}
ENV JAVA_HOME /etc/alternatives/jre

# Agent bond including Jolokia and jmx_exporter
ADD agent-bond-opts /opt/run-java-options
RUN mkdir -p /opt/agent-bond
ADD maven/agent-bond-agent-1.2.0.jar /opt/agent-bond/agent-bond.jar

RUN chmod 444 /opt/agent-bond/agent-bond.jar \
    && chmod 755 /opt/run-java-options

ADD jmx_exporter_config.yml /opt/agent-bond/

# Add run script as /deployments/run-java.sh and make it executable
COPY run-java.sh /deployments/
RUN chmod 755 /deployments/run-java.sh
ENV PATH="/deployments:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

COPY run-java-options /opt/run-java-options

RUN chmod +x /opt/run-java-options

RUN mkdir -p /deployments/options.d

ADD options.d /deployments/

CMD [ "/deployments/run-java.sh" ]
