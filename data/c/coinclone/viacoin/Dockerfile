FROM debian:jessie  
  
WORKDIR /root/  
  
COPY config/run.sh /root/  
COPY config/get_pub_key.py /root/  
  
RUN echo 'deb-src ftp://ftp.us.debian.org/debian/ sid main contrib non-free'
>> /etc/apt/sources.list && \  
apt-get update && \  
apt-get build-dep -y \  
bitcoin && \  
apt-get --install-recommends install -y \  
libbitcoin-dev && \  
apt-get install -y \  
# vim \  
git && \  
rm -rf /var/lib/apt/lists/* && \  
\  
cd $HOME && \  
git clone https://github.com/coinclone/viacoin.git && \  
\  
cd $HOME/viacoin && \  
autoreconf --install && \  
aclocal && \  
automake --add-missing && \  
./configure --with-incompatible-bdb --with-gui=no --with-qrencode=no && \  
make  
  
ENTRYPOINT ["bash", "/root/run.sh"]  
CMD ["viacoin"]  

