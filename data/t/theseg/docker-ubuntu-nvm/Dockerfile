# docker-nvm-base  
FROM ubuntu:xenial  
MAINTAINER John *Seg* Seggerson <seg@segonmedia.com>  
  
RUN rm /bin/sh && ln -s /bin/bash /bin/sh  
  
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \  
apt-get install -y git \  
zip \  
curl \  
build-essential \  
libssl-dev \  
gawk \  
libreadline6-dev \  
libyaml-dev \  
libsqlite3-dev\  
sqlite3 \  
autoconf \  
libgmp-dev \  
libgdbm-dev \  
libncurses5-dev \  
automake \  
libtool \  
bison \  
pkg-config \  
libffi-dev \  
automake \  
nasm \  
libpng-dev\  
libwebp-dev \  
libmysqlclient-dev \  
postgresql-client \  
python \  
python-dev \  
python-pip \  
python-virtualenv && \  
rm -rf /var/lib/apt/lists/*  
  
ENV NVM_DIR /usr/local/.nvm  
ENV NODE_VERSION stable  
  
# Install nvm  
RUN git clone https://github.com/creationix/nvm.git $NVM_DIR && \  
cd $NVM_DIR && \  
git checkout `git describe --abbrev=0 --tags`  
  
# Install default version of Node.js  
RUN source $NVM_DIR/nvm.sh && \  
nvm install $NODE_VERSION && \  
nvm install lts/boron && \  
nvm install lts/carbon && \  
nvm alias default $NODE_VERSION && \  
nvm use default  
  
# Add nvm.sh to .bashrc for startup...  
RUN echo "source ${NVM_DIR}/nvm.sh" > $HOME/.bashrc && \  
source $HOME/.bashrc  
  
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules  
  
# Install RVM for Ruby  
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys
409B6B1796C275462A1703113804BB82D39DC0E3  
RUN curl -sSL https://get.rvm.io | bash  
  
# Install latest Ruby version.  
RUN /bin/bash -l -c "rvm requirements"  
RUN /bin/bash -l -c "rvm install ruby"  
RUN /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"  
RUN /bin/bash -l -c "gem install sass --no-rdoc --no-ri"  
  
# Set the path.  
ENV PATH $NVM_DIR/v$NODE_VERSION/bin:$PATH  
  
# Update/Install PIP's  
RUN pip install --upgrade pip  
RUN pip install -U $(pip freeze | cut -d '=' -f 1)  
RUN pip install awscli  

