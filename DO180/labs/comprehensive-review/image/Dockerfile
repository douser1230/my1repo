FROM ubi7/ubi:7.7
MAINTAINER joedo doj@server.com
ARG NEXUS_VERSION=2.14.3-02
ENV NEXUS_HOME=/opt/nexus
#COPY training.repo /etc/yum.repos.d 
RUN yum install -y --setopt=tsflags=nodocs java-1.8.0-openjdk-devel && yum clean all -y
RUN groupadd -g 1001 nexus && \
    useradd -u 1001 -g nexus -m -d ${NEXUS_HOME} -s /sbin/nologin nexus && \
	chown -R nexus.nexus ${NEXUS_HOME} && \
	chmod -R 755 ${NEXUS_HOME}
ADD nexus-${NEXUS_VERSION}-bundle.tar.gz ${NEXUS_HOME}
ADD nexus-start.sh ${NEXUS_HOME}/
RUN ln -s ${NEXUS_HOME}/nexus-${NEXUS_VERSION} ${NEXUS_HOME}/nexus2
USER nexus
WORKDIR ${NEXUS_HOME}
VOLUME ["/opt/nexus/sonatype-work"]
CMD ["sh", "nexus-start.sh"] 

