FROM electronuserland/electron-builder:4  
  
# libgnome-keyring-dev — to build keytar  
RUN apt-key adv --keyserver keyserver.ubuntu.com \--recv-keys F9CB8DB0 && \  
echo "deb http://ppa.launchpad.net/ubuntu-wine/ppa/ubuntu xenial main " | tee
/etc/apt/sources.list.d/wine.list && \  
dpkg --add-architecture i386 && \  
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \--recv-keys
3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \  
echo "deb http://download.mono-project.com/repo/debian wheezy main" | tee
/etc/apt/sources.list.d/mono-xamarin.list && \  
apt-get update -y && \  
apt-get install -y \--no-install-recommends wine1.8 mono-devel ca-
certificates-mono git jq openssh-client && \  
apt-get clean && rm -rf /var/lib/apt/lists/*  
  
ENV WINEDEBUG -all,err+all  
  
RUN wineboot --init || true  

