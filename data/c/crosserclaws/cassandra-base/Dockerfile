FROM ubuntu:14.04  
# Install Java.  
RUN \  
apt-get update && \  
apt-get install -y software-properties-common && \  
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true |
debconf-set-selections && \  
add-apt-repository -y ppa:webupd8team/java && \  
apt-get update && \  
apt-get install -y oracle-java8-installer && \  
rm -rf /var/cache/oracle-jdk8-installer && \  
rm -rf /var/lib/apt/lists/*  
# ########################################  
# Common environment  
# ########################################  
ENV TZ Asia/Taipei  
ENV PROJ_ROOT /opt  
# :~)  

