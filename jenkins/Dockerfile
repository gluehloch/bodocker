# awtools Jenkins 
# docker build -t jenkins-awtools:latest .
# docker run --name jenkins-test -d -p 8888:8080 -p 50000:50000 -v jenkins-home:/var/jenkins_home jenkins-test:latest
# docker run --name jenkins-test -d -p 8888:8080 -p 50000:50000 -v /c/Users/winkler/.m2:/var/maven -v jenkins-home:/var/jenkins_home jenkins-test:latest
# docker exec -u root  -it jenkins-lts-2 bash

FROM jenkins/jenkins:lts

LABEL maintainer="Andre Winkler"
LABEL mail="andre.winkler@web.de"

ARG MAVEN_VERSION=3.6.0
# ARG USER_HOME_DIR="/home/developer"
# ARG SHA=707b1f6e390a65bde4af4cdaf2a24d45fc19a6ded00fff02e91626e3e42ceaff
# ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
  vim \
  curl \
  wget \
  && useradd -m developer

RUN curl -sL https://deb.nodesource.com/setup_10.x -o /tmp/nodesource_setup.sh \
  && chmod u+x /tmp/nodesource_setup.sh \
  && /tmp/nodesource_setup.sh \
  && apt-get install -y --no-install-recommends nodejs

RUN curl -sL https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz \
  -o /tmp/openjdk-11.0.2_linux-x64_bin.tar.gz \
  && gunzip /tmp/openjdk-11.0.2_linux-x64_bin.tar.gz \
  && tar xvf /tmp/openjdk-11.0.2_linux-x64_bin.tar \
  && mv jdk-11.0.2/ /opt \
  && chown -R jenkins:jenkins /opt/jdk-11.0.2

RUN curl -sL http://ftp-stud.hs-esslingen.de/pub/Mirrors/ftp.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz \
  -o /tmp/apache-maven-3.6.0-bin.tar.gz \
  && gunzip /tmp/apache-maven-3.6.0-bin.tar.gz \
  && tar xvf /tmp/apache-maven-3.6.0-bin.tar \
  && mv apache-maven-3.6.0 /opt \
  && chown -R jenkins:jenkins /opt/apache-maven-3.6.0

USER jenkins
