FROM maksatsoftware/ubuntu  
  
MAINTAINER Maksat Annageldyev <maksat.annageldyev@maksat.software>  
  
ENV DEBIAN_FRONTEND noninteractive  
ENV INITRD No  
ENV LANG en_US.UTF-8  
RUN apt-get update && \  
apt-get install --no-install-recommends -y openjdk-8-jre-headless && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
CMD ["/usr/bin/java"]  

