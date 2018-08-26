FROM sonarqube:6.3
MAINTAINER Amulya P Malla  <amulyapmalla@gmail.com>

# update the package sources, clamd
RUN apt-get update --fix-missing \
    && apt-get install -y \
    clamdscan \
    libclamav-dev \ 
    vim openssh-server software-properties-common net-tools 
    
ENV SONAR_DOWNLOAD_URL https://sonarsource.bintray.com/Distribution
ENV SONAR_SCANNER_VERSION 3.2.0.1227 
ENV SONAR_SCANNER_HOME /opt/sonarqube/sonar-scanner-${SONAR_SCANNER_VERSION}-linux

# Installing Plugins
RUN cd /opt/sonarqube/extensions/plugins/
RUN curl -o sonar-java-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-java-plugin/sonar-java-plugin-4.8.0.9441.jar
RUN curl -o sonar-web-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-web-plugin/sonar-web-plugin-2.5.0.476.jar
RUN curl -o sonar-scm-git-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-scm-git-plugin/sonar-scm-git-plugin-1.2.jar
RUN curl -o sonar-csharp-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-csharp-plugin/sonar-csharp-plugin-5.8.0.660.jar
RUN curl -o sonar-javascript-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-javascript-plugin/sonar-javascript-plugin-2.21.1.4786.jar
RUN curl -o sonar-php-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-php-plugin/sonar-php-plugin-2.10.0.2087.jar
RUN curl -o sonar-checkstyle-plugin.jar -fSL $SONAR_DOWNLOAD_URL/sonar-checkstyle-plugin/sonar-checkstyle-plugin-2.4.jar
RUN curl -o sonar-xml-plugin-1.4.3.1027.jar -fSL $SONAR_DOWNLOAD_URL/sonar-xml-plugin/sonar-xml-plugin-1.4.3.1027.jar
RUN curl -o sonar-typescript-plugin-1.1.0.1079.jar -fSL $SONAR_DOWNLOAD_URL/sonar-typescript-plugin/sonar-typescript-plugin-1.1.0.1079.jar

# # Add Scala Plugin - https://github.com/ncredinburgh/sonar-scalastyle
# ADD plugins/sonar-scalastyle-0.0.3-SNAPSHOT.jar /opt/sonarqube/extensions/plugins/

# # Add Kotlin Plugin - https://github.com/K0zka/kotlin-sonar
# ADD plugins/kotlin-sonar-0.1-SNAPSHOT.jar /opt/sonarqube/extensions/plugins/

# # Add default Java Quality Profile
# ADD qualityprofile/java-standardprofile.xml /qualityprofile/

# VOLUME ["$SONARQUBE_HOME/data", "$SONARQUBE_HOME/extensions", "/qualityprofile"]

VOLUME ["$SONARQUBE_HOME/data"]
ADD start_sonarqube.sh /opt/sonarqube/start_sonarqube.sh
ENTRYPOINT ["/opt/sonarqube/start_sonarqube.sh"]
