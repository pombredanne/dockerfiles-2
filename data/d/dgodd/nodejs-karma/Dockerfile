FROM ubuntu:trusty  
  
MAINTAINER Dave Goddard <dave@goddard.id.au>  
  
ENV TERM dummy  
  
RUN apt-get update; \  
apt-get install -y git curl; \  
curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -; \  
curl https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add
- ; \  
sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >>
/etc/apt/sources.list.d/google.list'; \  
apt-get update && apt-get install -y google-chrome-stable nodejs Xvfb python
build-essential; \  
apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
ADD xvfb.sh /etc/init.d/xvfb  
ADD entrypoint.sh /entrypoint.sh  
  
ENV DISPLAY :99.0  
ENV CHROME_BIN /usr/bin/google-chrome  
  
RUN mkdir /nodemodules  
ADD package.json /nodemodules/package.json  
WORKDIR /nodemodules  
RUN npm install  
  
WORKDIR /  
ENTRYPOINT ["/entrypoint.sh"]  

