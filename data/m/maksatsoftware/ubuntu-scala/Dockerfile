FROM maksatsoftware/ubuntu-java  
  
MAINTAINER Maksat Annageldyev <maksat.annageldyev@maksat.software>  
  
ENV DEBIAN_FRONTEND noninteractive  
ENV INITRD No  
ENV LANG en_US.UTF-8  
ENV SCALA_VERSION 2.11.8  
RUN echo 'deb http://dl.bintray.com/sbt/debian /' \  
| tee /etc/apt/sources.list.d/sbt.list && \  
apt-get update && \  
apt-get install --no-install-recommends -y --force-yes sbt && \  
wget http://www.scala-lang.org/files/archive/scala-$SCALA_VERSION.deb && \  
dpkg -i scala-$SCALA_VERSION.deb && rm scala-$SCALA_VERSION.deb && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
CMD ["scala"]  

