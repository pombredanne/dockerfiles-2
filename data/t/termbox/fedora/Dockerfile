FROM fedora:25  
  
ENV TERM=xterm-256color  
  
RUN dnf update -y && \  
dnf install -y \  
@development-tools \  
abduco nano vim procps-ng \  
iproute traceroute \  
git subversion \  
nodejs npm \  
ruby rubygem-bundler \  
golang \  
rust cargo \  
python3 python3-pip  
  
CMD ["abduco", "-A", "termbox", "bash"]  

