FROM ubuntu:latest  
  
MAINTAINER Maksat Annageldyev <maksat.annageldyev@maksat.software>  
  
ENV DEBIAN_FRONTEND noninteractive  
ENV INITRD No  
ENV LANG en_US.UTF-8  
RUN apt-get update && \  
apt-get upgrade -y && \  
apt-get install -y --no-install-recommends \  
vim.tiny wget curl sudo net-tools pwgen \  
git-core logrotate software-properties-common && \  
locale-gen en_US en_US.UTF-8 && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
CMD ["bash"]  

