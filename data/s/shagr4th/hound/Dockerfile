FROM alpine:3.4  
ENV GOPATH /go  
  
COPY . /go/src/github.com/etsy/hound  
  
COPY default-config.json /data/config.json  
  
RUN apk update \  
&& apk add go git subversion mercurial bzr openssh \  
&& go install github.com/etsy/hound/cmds/houndd \  
&& apk del go \  
&& rm -f /var/cache/apk/* \  
&& rm -rf /go/src /go/pkg  
  
VOLUME ["/data"]  
  
EXPOSE 6080  
ENTRYPOINT ["/go/bin/houndd", "-conf", "/data/config.json"]  

