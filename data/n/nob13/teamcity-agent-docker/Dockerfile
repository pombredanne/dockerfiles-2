FROM ubuntu:14.04  
ENV AGENT_DIR /opt/buildAgent  
  
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \  
lxc iptables aufs-tools ca-certificates curl wget software-properties-common
language-pack-en \  
&& rm -rf /var/lib/apt/lists/*  
  
# Fix locale.  
ENV LANG en_US.UTF-8  
ENV LC_CTYPE en_US.UTF-8  
RUN locale-gen en_US && update-locale LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8  
  
# grab gosu for easy step-down from root  
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys
B42F6819007F00F88E364FD4036A9C25BF357DD4  
RUN curl -o /usr/local/bin/gosu -SL
"https://github.com/tianon/gosu/releases/download/1.6/gosu-$(dpkg --print-
architecture)" \  
&& curl -o /usr/local/bin/gosu.asc -SL
"https://github.com/tianon/gosu/releases/download/1.6/gosu-$(dpkg --print-
architecture).asc" \  
&& gpg --verify /usr/local/bin/gosu.asc \  
&& rm /usr/local/bin/gosu.asc \  
&& chmod +x /usr/local/bin/gosu  
  
# Install java-8-oracle  
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-
set-selections \  
&& echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-
selections \  
&& add-apt-repository -y ppa:webupd8team/java \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends \  
oracle-java8-installer ca-certificates-java \  
&& rm -rf /var/lib/apt/lists/* /var/cache/oracle-jdk8-installer/*.tar.gz
/usr/lib/jvm/java-8-oracle/src.zip /usr/lib/jvm/java-8-oracle/javafx-src.zip \  
/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts \  
&& ln -s /etc/ssl/certs/java/cacerts
/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts \  
&& update-ca-certificates  
  
# Install docker  
RUN wget -O /usr/local/bin/docker
https://get.docker.com/builds/Linux/x86_64/docker-1.9.1 && chmod +x
/usr/local/bin/docker  
  
RUN groupadd docker && adduser --disabled-password --gecos "" teamcity --home
/opt/buildAgent \  
&& sed -i -e "s/%sudo.*$/%sudo ALL=(ALL:ALL) NOPASSWD:ALL/" /etc/sudoers \  
&& usermod -a -G docker,sudo teamcity  
  
# Install jq (from github, repo contains ancient version)  
RUN curl -o /usr/local/bin/jq -SL
https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 \  
&& chmod +x /usr/local/bin/jq  
  
# Install ruby and node.js build repositories  
RUN apt-add-repository ppa:chris-lea/node.js \  
&& apt-add-repository ppa:brightbox/ruby-ng \  
&& apt-get update \  
&& apt-get upgrade -y \  
&& apt-get install -y nodejs ruby2.1 ruby2.1-dev ruby ruby-switch unzip \  
iptables lxc fontconfig libffi-dev build-essential git python-dev libssl-dev
python-pip \  
psmisc \  
&& rm -rf /var/lib/apt/lists/*  
  
# Somehow broken, we don't need it  
# # Install httpie (with SNI), awscli, docker-compose  
# RUN pip install --upgrade pyopenssl pyasn1 ndg-httpsclient httpie awscli
docker-compose==1.5.1  
# RUN ruby-switch --set ruby2.1  
# RUN npm install -g bower grunt-cli  
# RUN gem install rake bundler compass --no-ri --no-rdoc  
# Install MongoDB Server (it will not run, but executable will be there)  
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 \  
&& echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0
multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list \  
&& apt-get update \  
&& apt-get install -y mongodb-org-server  
  
# Add Reactive Core CA  
RUN curl https://www.reactivecore.de/files/reactivecore.ca.crt >
/usr/local/share/ca-certificates/reactivecore.ca.crt && update-ca-certificates  
  
# Install PhantomJS (See: https://gist.github.com/julionc/7476620)  
ENV PHANTOM_JS="phantomjs-1.9.8-linux-x86_64"  
RUN apt-get install -y build-essential chrpath libssl-dev libxft-dev
libfreetype6 libfreetype6-dev libfontconfig1 libfontconfig1-dev \  
&& wget https://bitbucket.org/ariya/phantomjs/downloads/$PHANTOM_JS.tar.bz2 \  
&& mv $PHANTOM_JS.tar.bz2 /usr/local/share/; cd /usr/local/share/; tar xvjf
$PHANTOM_JS.tar.bz2 \  
&& ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/local/bin/phantomjs
\  
&& ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/bin/phantomjs  
  
# Install Extra Tools(CMAKE, make, etc.)  
RUN apt-get install -y cmake build-essential  
  
# Install the magic wrapper.  
ADD wrapdocker /usr/local/bin/wrapdocker  
  
ADD docker-entrypoint.sh /docker-entrypoint.sh  
  
ENTRYPOINT ["/docker-entrypoint.sh"]  
  
VOLUME /var/lib/docker  
VOLUME /opt/buildAgent  
VOLUME /data  
  
EXPOSE 9090  

