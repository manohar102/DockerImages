FROM centos:7

WORKDIR /opt

RUN curl -O https://cdn.azul.com/zulu/bin/zulu-repo-1.0.0-1.noarch.rpm
RUN sudo rpm --import https://www.azul.com/wp-content/uploads/2021/05/0xB1998361219BD9C9.txt
RUN sudo zypper install zulu-repo-1.0.0-1.noarch.rpm
RUN sudo zypper install zulu11-jdk

RUN export JAVA_HOME = "/usr/lib/jvm/zulu11"
RUN export PATH=${PATH}:${JAVA_HOME}/bin

RUN sudo yum install maven



