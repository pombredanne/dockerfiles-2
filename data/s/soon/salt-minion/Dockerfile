#  
# Salt Stack Salt Master Container  
#  
FROM ubuntu:14.04  
MAINTAINER SOON_ <dorks@thisissoon.com>  
  
# Update System  
RUN apt-get update && apt-get upgrade -y -o DPkg::Options::=--force-confold  
  
# Install Development Vdersion @ 2014.7  
# See: https://github.com/saltstack/salt-bootstrap/issues/394  
ADD https://bootstrap.saltstack.com /usr/local/bin/install_salt.sh  
RUN chmod +x /usr/local/bin/install_salt.sh  
ADD relay.sh /usr/local/bin/relay.sh  
RUN chmod +x /usr/local/bin/relay.sh  
RUN relay.sh install_salt.sh git v2014.7  
  
# Volumes  
VOLUME ['/etc/salt/minion.d', ]  
  
# Add Run File  
ADD run.sh /usr/local/bin/run.sh  
RUN chmod +x /usr/local/bin/run.sh  
  
# Run Command  
CMD "/usr/local/bin/run.sh"  

