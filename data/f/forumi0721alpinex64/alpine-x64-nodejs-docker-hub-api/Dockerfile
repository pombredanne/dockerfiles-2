FROM forumi0721alpinex64/alpine-x64-nodejs:latest  
  
MAINTAINER stonecold <forumi0721@gmail.com>  
  
COPY local/. /usr/local/  
  
#RUN ["docker-build-start"]  
RUN ["docker-init"]  
  
#RUN ["docker-build-end"]  
ENTRYPOINT ["docker-run"]  
  

