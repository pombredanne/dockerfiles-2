# fortune  
#  
  
FROM debian:wheezy  
MAINTAINER Mike  
  
RUN apt-get update \  
&& apt-get install -y --force-yes fortune \  
#  
# clean up  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
  
ENV PATH /usr/games:$PATH  
  
ENTRYPOINT ["fortune"]  

