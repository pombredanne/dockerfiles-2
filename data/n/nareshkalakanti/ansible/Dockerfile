FROM ubuntu:trusty  
MAINTAINER naresh <naresh.kalakanti@gmail.com>  
  
# Prevent dpkg errors  
ENV TERM=xterm-256color  
  
# Set mirrors to NZ  
RUN sed -i "s/http:\/\/archive./http:\/\/nz.archive./g" /etc/apt/sources.list  
  
# Install Ansible  
RUN apt-get update -qy && \  
apt-get install -qy software-properties-common && \  
apt-add-repository -y ppa:ansible/ansible && \  
apt-get update -qy && \  
apt-get install -qy ansible  
  
# Add Volume for Ansible playbooks  
VOLUME /ansible  
WORKDIR /ansible  
  
# Add entrypoint script  
ENTRYPOINT ["entrypoint.sh"]  
CMD ["site.yml"]  

