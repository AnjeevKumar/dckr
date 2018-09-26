FROM debian:jessie
MAINTAINER Amulya P Malla  <amulyapmalla@gmail.com>

# update the package sources, clamd
RUN apt-get update --fix-missing \
    && apt-get install -y \
    clamdscan \
    libclamav-dev \
    curl wget git htop supervisor vim openssh-server software-properties-common net-tools unzip
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

# JMeter Installation
# Environment Variable                 
ARG JMETER_VERSION=3.3
ENV JMETER_PLUGINS_VERSION=1.4.0

# Install jmeter
RUN   mkdir /jmeter \
      && cd /jmeter/ \
      && wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-$JMETER_VERSION.tgz \
      && tar -xzf apache-jmeter-$JMETER_VERSION.tgz \
      && rm apache-jmeter-$JMETER_VERSION.tgz \
	  && mkdir /jmeter-plugins \
	  && cd /jmeter-plugins/ \
	  && wget https://jmeter-plugins.org/downloads/file/JMeterPlugins-ExtrasLibs-${JMETER_PLUGINS_VERSION}.zip \
	  && unzip -o JMeterPlugins-ExtrasLibs-${JMETER_PLUGINS_VERSION}.zip -d /jmeter/apache-jmeter-$JMETER_VERSION/

# Set Jmeter Home
ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

# Add Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH
