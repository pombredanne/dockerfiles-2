FROM twolf/alpine2:latest  
MAINTAINER Thomas Boerger <thomas@webhippie.de>  
  
ENV MINECRAFT_VERSION 1.7.10  
ENV MINECRAFT_URL
https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/minecraft_server.${MINECRAFT_VERSION}.jar  
ENV MINECRAFT_JAR minecraft_server.${MINECRAFT_VERSION}.jar  
  
ENV SERVER_MAXHEAP 2048M  
ENV SERVER_MINHEAP 512M  
ENV SERVER_MAXPERM 128M  
ENV SERVER_OPTS nogui  
ENV SERVER_MOTD Minecraft  
ENV SERVER_RCONPWD webhippie  
  
RUN apk add --update \  
curl \  
vim \  
ca-certificates \  
nss \  
openjdk7 && \  
rm -rf /var/cache/apk/* && \  
mkdir -p /minecraft && \  
curl -sSLo /minecraft/${MINECRAFT_JAR} ${MINECRAFT_URL} 2> /dev/null  
  
VOLUME ["/minecraft/merge", "/minecraft/world", "/minecraft/logs"]  
  
ADD rootfs /  
EXPOSE 25565 25575  
WORKDIR /minecraft  
CMD ["/usr/bin/s6-svscan","/etc/s6"]  

