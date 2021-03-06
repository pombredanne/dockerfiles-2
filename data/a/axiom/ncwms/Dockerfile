FROM unidata/tomcat-docker:8.5  
MAINTAINER Kyle Wilcox <kyle@axiomdatascience.com>  
  
RUN \  
apt-get update && \  
apt-get install -y \  
git \  
maven \  
unzip \  
&& \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
# Fix for java8 in jessie  
# https://serverfault.com/questions/830636/cannot-install-openjdk-8-jre-
headless-on-debian-jessie/830637#830637  
# https://askubuntu.com/questions/190582/installing-java-automatically-with-
silent-option  
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial
main\ndeb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" >
/etc/apt/sources.list.d/webupd8team-java.list && \  
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 &&
\  
apt-get update && \  
echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-
selections && \  
echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-
selections && \  
apt-get install -y oracle-java8-installer && \  
update-java-alternatives -s java-8-oracle && \  
export JAVA_HOME=/usr/lib/jvm/java-8-oracle  
  
ENV EDAL_VERSION rework-rebase-killroy  
# Compile edal to use required features in dev branch  
RUN mkdir /edal && \  
cd /edal && \  
git clone https://github.com/axiom-data-science/edal-java.git && \  
cd edal-java && \  
git checkout ${EDAL_VERSION} && \  
JAVA_HOME=/usr/lib/jvm/java-8-oracle mvn clean install  
  
# Cache some dependencies  
COPY pom.xml .  
RUN mvn clean test dependency:go-offline  
  
# Compile and install ncWMS  
COPY . /ncWMS  
RUN cd /ncWMS && \  
JAVA_HOME=/usr/lib/jvm/java-8-oracle mvn clean install && \  
mkdir -p /srv/ncwms && \  
unzip target/ncWMS2.war -d /srv/ncwms/ && \  
rm -rf /edal && \  
rm -rf /ncWMS/target  
  
# Set login-config to BASIC since it is handled through Tomcat  
RUN sed -i -e 's/DIGEST/BASIC/' /srv/ncwms/WEB-INF/web.xml && \  
cp /ncWMS/config/setenv.sh $CATALINA_HOME/bin/setenv.sh && \  
cp /ncWMS/config/tc-ehcache.xml $CATALINA_HOME/conf/tc-ehcache.xml && \  
cp /ncWMS/config/tomcat-users.xml $CATALINA_HOME/conf/tomcat-users.xml && \  
mkdir -p $CATALINA_HOME/conf/Catalina/localhost/ && \  
mkdir -p $CATALINA_HOME/.ncWMS2 && \  
cp /ncWMS/config/config.xml $CATALINA_HOME/.ncWMS2/config.xml  
  
RUN echo '<?xml version="1.0" encoding="UTF-8"?>\n<Context
docBase="/srv/ncwms" path="" />' \  
> $CATALINA_HOME/conf/Catalina/localhost/ROOT.xml  
  
ENTRYPOINT ["/ncWMS/entrypoint.sh"]  
  
EXPOSE 8080 8443 9090  
CMD ["catalina.sh", "run"]  
  
HEALTHCHECK \--interval=2m --timeout=1s --retries=3 \  
CMD curl -fsIo /dev/null
"http://localhost:8080/wms?REQUEST=GetLegendGraphic&COLORBARONLY=true" || exit
1  

