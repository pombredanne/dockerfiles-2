FROM golang:latest as builder  
  
MAINTAINER t@hitian.info  
  
RUN mkdir /usr/bin/v2ray/  
RUN mkdir /etc/v2ray/  
RUN mkdir /var/log/v2ray/  
RUN go get -u v2ray.com/core/...  
RUN go get -u v2ray.com/ext/...  
RUN go install v2ray.com/ext/tools/build/vbuild  
RUN vbuild -dir /usr/bin/v2ray --os=linux --arch=arm  
  
FROM arm32v6/alpine:latest  
COPY \--from=builder /usr/bin/v2ray /usr/bin/v2ray  
ENV PATH /usr/bin/v2ray/:$PATH  
CMD ["v2ray", "-h"]  
  

