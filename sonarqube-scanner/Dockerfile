FROM debian:jessie
MAINTAINER Amulya P Malla  <amulyapmalla@gmail.com>

# update the package sources, clamd
RUN apt-get update --fix-missing \
    && apt-get install -y \
    clamdscan \
    libclamav-dev \
    curl wget  htop  vim openssh-server software-properties-common netcat net-tools unzip

# Java Installation 
RUN \
    echo "===> add webupd8 repository..."  && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list  && \
    echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list  && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886  && \
    apt-get update  && \
    \
    \
    echo "===> install Java"  && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections  && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections  && \
    DEBIAN_FRONTEND=noninteractive  apt-get install -y --force-yes oracle-java8-installer oracle-java8-set-default  && \
    \
    \
    echo "===> clean up..."  && \
    rm -rf /var/cache/oracle-jdk8-installer  && \
    apt-get clean  && \
    rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

ENV PATH=${JAVA_HOME}/bin:$PATH      

# Sonar scanner Installation
ENV SONAR_DOWNLOAD_URL https://sonarsource.bintray.com/Distribution
ENV SONAR_SCANNER_VERSION 3.2.0.1227 
ENV SONAR_SCANNER_HOME /opt/sonarqube/sonar-scanner-${SONAR_SCANNER_VERSION}-linux

RUN mkdir -p /opt/sonarqube 
WORKDIR /opt/sonarqube/
RUN curl -o ./sonarscanner.zip -fSL $SONAR_DOWNLOAD_URL/sonar-scanner-cli/sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip \
    && unzip sonarscanner.zip \
    &&  rm sonarscanner.zip

ENV SONAR_RUNNER_HOME $SONAR_SCANNER_HOME
ENV PATH=${SONAR_RUNNER_HOME}/bin:$PATH

COPY  sonar-scanner.properties $SONAR_SCANNER_HOME/conf/sonar-scanner.properties
COPY sonar-scanner-run.sh /usr/bin
