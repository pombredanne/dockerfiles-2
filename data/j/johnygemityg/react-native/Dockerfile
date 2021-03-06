## -*- docker-image-name: "react-native" -*-  
# Docker image for react native experimentation  
FROM node:latest  
  
MAINTAINER Jan Pokorny  
  
# Setup environment variables  
ENV PATH $PATH:node_modules/.bin  
  
##  
## Install Java  
##  
RUN DEBIAN_FRONTEND=noninteractive apt-get update -q && \  
apt-get install -qy --no-install-recommends sudo default-jdk  
  
##  
## Install Android SDK  
##  
# Set correct environment variables.  
ENV ANDROID_SDK_FILE android-sdk_r24.0.1-linux.tgz  
ENV ANDROID_SDK_URL http://dl.google.com/android/$ANDROID_SDK_FILE  
  
# Install 32bit support for Android SDK  
RUN dpkg --add-architecture i386 && \  
apt-get update -q && \  
apt-get install -qy --no-install-recommends libstdc++6:i386 libgcc1:i386
zlib1g:i386 libncurses5:i386  
  
# Install kvm support for Android emulator  
#RUN apt-get install -qy --no-install-recommends qemu-kvm libvirt-bin
libegl1-mesa  
# Install Android SDK  
ENV ANDROID_HOME /usr/local/android-sdk-linux  
RUN cd /usr/local && \  
wget $ANDROID_SDK_URL && \  
tar -xzf $ANDROID_SDK_FILE && \  
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools && \  
chgrp -R users $ANDROID_HOME && \  
chmod -R 0775 $ANDROID_HOME && \  
rm $ANDROID_SDK_FILE  
  
# Install android tools and system-image.  
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-
tools:$ANDROID_HOME/build-tools/23.0.1  
RUN apt-get install expect -y --force-yes  
COPY tools /opt/tools  
RUN ["/opt/tools/android-accept-licenses.sh", "android update sdk --all --no-
ui --filter platform-tools,android-23,build-tools-23.0.1,extra-android-
support,extra-android-m2repository,sys-img-x86_64-android-23,extra-
google-m2repository"]  
  
#Download better node  
RUN npm install -g n  
RUN n stable  
  
##  
## Install react native  
##  
RUN npm install -g react-native-cli  
  
# Clean up when done.  
RUN apt-get clean && \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \  
npm cache clear  
  
# Default react-native web server port  
EXPOSE 8081  
ENV USERNAME dev  
  
RUN adduser --disabled-password --gecos '' $USERNAME && \  
echo $USERNAME:$USERNAME | chpasswd && \  
echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \  
adduser $USERNAME sudo  
#adduser $USERNAME kvm && \  
#adduser $USERNAME libvirt  
# Create android avd image  
# RUN echo "no" | android create avd -n android-23-phone -c 1000M -s WVGA854
-t 1  
# Tell gradle to store dependencies in a sub directory of the android project  
# this persists the dependencies between builds  
ENV GRADLE_USER_HOME /home/$USERNAME/app/android/gradle_deps  
  
USER $USERNAME  
  
# Set workdir  
# You'll need to run this image with a volume mapped to /home/dev (i.e. -v
$(pwd):/home/dev) or override this value  
WORKDIR /home/$USERNAME/app  
  

