# Based on
https://raw.githubusercontent.com/apache/nutch/master/docker/Dockerfile  
FROM java:8  
MAINTAINER smartive AG <hello@smartive.ch>  
  
ENV NUTCH_HOME /root/nutch  
ENV PHANTOM_JS phantomjs-2.1.1-linux-x86_64  
  
WORKDIR /root/  
  
# Get the package containing apt-add-repository installed for adding
repositories  
RUN apt-get update && \  
apt-get upgrade -y  
  
# Add the repository that we'll pull java down from.  
#RUN add-apt-repository -y ppa:webupd8team/java && apt-get update && apt-get
upgrade -y  
# Get Oracle Java 1.7 installed  
#RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select
true | /usr/bin/debconf-set-selections && apt-get install -y oracle-
java7-installer oracle-java7-set-default  
# Install various dependencies  
RUN apt-get install -y \  
ant \  
openssh-server \  
vim \  
telnet \  
git \  
rsync \  
curl \  
build-essential \  
chrpath \  
libssl-dev \  
libxft-dev \  
libfreetype6 \  
libfreetype6-dev \  
libfontconfig1 \  
libfontconfig1-dev  
  
# Set up JAVA_HOME  
#RUN echo 'export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:bin/java::")'
>> $HOME/.bashrc  
# Install PhantomJS  
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/$PHANTOM_JS.tar.bz2
&& \  
tar xvjf $PHANTOM_JS.tar.bz2 && \  
mv $PHANTOM_JS /usr/local/share && \  
ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/local/bin  
  
# Checkout and build the nutch trunk  
RUN wget https://github.com/apache/nutch/archive/master.zip && unzip
master.zip && mv nutch-master nutch_source && cd nutch_source && ant  
  
# Convenience symlink to Nutch runtime local  
RUN ln -s nutch_source/runtime/local $NUTCH_HOME  
  
ADD startup.sh /root/startup.sh  
RUN chmod +x /root/startup.sh  
  
ENTRYPOINT ["/root/startup.sh"]  

