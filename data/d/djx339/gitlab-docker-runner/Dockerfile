FROM djx339/gitlab-docker-runner  
  
RUN apt-get update && apt-get install -y --no-install-recommends \  
g++ \  
gcc \  
libc6-dev \  
make \  
&& rm -rf /var/lib/apt/lists/*  
  
ENV GOLANG_VERSION 1.5.2  
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-
amd64.tar.gz  
ENV GOLANG_DOWNLOAD_SHA1 cae87ed095e8d94a81871281d35da7829bd1234e  
  
RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \  
&& echo "$GOLANG_DOWNLOAD_SHA1 golang.tar.gz" | sha1sum -c - \  
&& tar -C /usr/local -xzf golang.tar.gz \  
&& rm golang.tar.gz  
  
ENV GOPATH /go  
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH  
  
RUN echo "export PATH=$PATH" >> /etc/profile \  
&& echo "export GOPATH=$GOPATH" >> /etc/profile  
  
RUN go get github.com/tools/godep  

