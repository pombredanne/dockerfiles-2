FROM amazonlinux:latest  
LABEL maintainer="sean@sean.io"  
  
RUN yum -y install passwd upstart util-linux curl gnupg2 initscripts iptables
iputils lsof nc net-tools nmap openssl procps strace tcpdump telnet vim wget
which; yum -y clean all; rm -rf /var/log/*  
# currently causes failures in travis, but no where else  
# RUN echo -e "NETWORKING=yes\nHOSTNAME=localhost.localdomain\nNOZEROCONF=yes"
>/etc/sysconfig/network  
CMD [ "/sbin/init" ]  

