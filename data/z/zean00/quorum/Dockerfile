FROM ubuntu:16.04 as builder  
  
WORKDIR /work  
  
RUN apt-get update && \  
apt-get install -y \  
build-essential \  
git \  
libdb-dev \  
libsodium-dev \  
libtinfo-dev \  
sysvbanner \  
unzip \  
wget \  
wrk \  
zlib1g-dev  
  
ENV CREL constellation-0.2.0-ubuntu1604  
  
RUN wget -q
https://github.com/jpmorganchase/constellation/releases/download/v0.2.0/$CREL.tar.xz
&& \  
tar xfJ $CREL.tar.xz && \  
cp $CREL/constellation-node /usr/local/bin && chmod 0755
/usr/local/bin/constellation-node && \  
rm -rf $CREL.tar.xz $CREL  
  
ENV GOREL go1.7.3.linux-amd64.tar.gz  
ENV PATH $PATH:/usr/local/go/bin  
  
RUN wget -q https://storage.googleapis.com/golang/$GOREL && \  
tar xfz $GOREL && \  
mv go /usr/local/go && \  
rm -f $GOREL  
  
RUN git clone https://github.com/jpmorganchase/quorum.git && \  
cd quorum && \  
git checkout tags/v2.0.0 && \  
make all && \  
cp build/bin/geth /usr/local/bin && \  
cp build/bin/bootnode /usr/local/bin && \  
cd .. && \  
rm -rf quorum  
  
### Create the runtime image, leaving most of the cruft behind (hopefully...)  
FROM ubuntu:16.04  
# Install add-apt-repository  
RUN apt-get update && \  
apt-get install -y --no-install-recommends software-properties-common && \  
add-apt-repository ppa:ethereum/ethereum && \  
apt-get update && \  
apt-get install -y --no-install-recommends \  
libdb-dev \  
libsodium-dev \  
libtinfo-dev \  
libleveldb-dev \  
iputils-ping \  
net-tools \  
vim \  
telnet \  
solc && \  
rm -rf /var/lib/apt/lists/*  
  
# Temporary useful tools  
# RUN apt-get update && \  
# apt-get install -y iputils-ping net-tools vim  
COPY \--from=builder \  
/usr/local/bin/constellation-node \  
/usr/local/bin/geth \  
/usr/local/bin/bootnode \  
/usr/local/bin/  
  
WORKDIR /qdata/dd/  
CMD ["/qdata/start-node.sh"]  

