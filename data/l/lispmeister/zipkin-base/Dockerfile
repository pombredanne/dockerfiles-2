FROM debian:sid  
MAINTAINER Markus Fix "http://deeprecursion.com"  
RUN apt-get update  
RUN apt-get install -y scala git curl  
RUN git clone https://github.com/twitter/zipkin.git  
RUN (cd zipkin; bin/sbt compile)  

