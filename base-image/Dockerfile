FROM centos:7

WORKDIR /opt

#
# UTF-8 by default
#
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

#
# Pull Zulu OpenJDK binaries from official repository:
#

ARG ZULU_REPO_VER=1.0.0-1

RUN rpm --import http://repos.azulsystems.com/RPM-GPG-KEY-azulsystems && \
    curl -sLO https://cdn.azul.com/zulu/bin/zulu-repo-${ZULU_REPO_VER}.noarch.rpm && \
    rpm -ivh zulu-repo-${ZULU_REPO_VER}.noarch.rpm && \
    yum -q -y update && \
    yum -q -y upgrade && \
    yum -q -y install yum-plugin-versionlock tzdata && \
    yum versionlock zulu11-*-11.0.17-* && \
    yum -q -y install zulu11-jdk && \
    yum clean all && \
    rm -rf /var/cache/yum zulu-repo_${ZULU_REPO_VER}.noarch.rpm

ENV JAVA_HOME=/usr/lib/jvm/zulu11
RUN export PATH=${PATH}:${JAVA_HOME}/bin

# Setting Maven Version that needs to be installed
ARG MAVEN_VERSION=3.5.4

# Changing user to root to install maven
USER root

# Install required tools
# which: otherwise 'mvn version' prints '/usr/share/maven/bin/mvn: line 93: which: command not found'
RUN yum update -y && \
  yum install -y which && \
  yum clean all

# Maven
RUN curl -fsSL https://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_VERSION=${MAVEN_VERSION}
ENV M2_HOME /usr/share/maven
ENV maven.home $M2_HOME
ENV M2 $M2_HOME/bin
ENV PATH $M2:$PATH

# Again using non-root user i.e. stakater as set in base image
USER 10001

# Define default command, can be overriden by passing an argument when running the container
CMD ["mvn","-version"]



