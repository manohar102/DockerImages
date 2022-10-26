FROM centos:7

WORKDIR /opt

RUN sudo yum install -y https://cdn.azul.com/zulu/bin/zulu-repo-1.0.0-1.noarch.rpm
RUN sudo yum install zulu11-jdk

RUN export JAVA_HOME = "/usr/lib/jvm/zulu11"
RUN export PATH=${PATH}:${JAVA_HOME}/bin

RUN sudo yum install maven



