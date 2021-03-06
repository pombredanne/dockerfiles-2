FROM alpine  
MAINTAINER The Goofball "goofball222@gmail.com"  
  
ARG BUILD_DATE  
ARG VCS_REF  
ARG VERSION  
  
LABEL \  
org.label-schema.vendor=goofball222 \  
org.label-schema.url="https://github.com/goofball222/murmur" \  
org.label-schema.name="Murmur Server" \  
org.label-schema.version=$VERSION \  
org.label-schema.vcs-url="https://github.com/goofball222/murmur.git" \  
org.label-schema.vcs-ref=$VCS_REF \  
org.label-schema.build-date=$BUILD_DATE \  
org.label-schema.license="Apache-2.0" \  
org.label-schema.schema-version="1.0"  
  
ENV \  
DEBUG=false \  
MURMUR_OPTS= \  
PGID=999 \  
PUID=999  
  
WORKDIR /opt/murmur  
  
COPY root /  
  
RUN set -x \  
&& delgroup ping \  
&& addgroup -g $PGID murmur \  
&& adduser -D -G murmur -u $PUID murmur \  
&& apk add --no-cache bash shadow \  
&& apk add --no-cache --virtual .build-deps curl \  
&& curl -sSL https://mumble.info/snapshot/murmur-static_x86-${VERSION}.tar.bz2
-o /tmp/murmur.tar.bz2 \  
&& tar -jxv -f /tmp/murmur.tar.bz2 \--strip-components=1 -C /opt/murmur \  
&& apk del .build-deps \  
&& bash -c 'mkdir -p {cert,config,data,log}' \  
&& mv /opt/murmur/murmur.ini /opt/murmur/murmur.ini-default \  
&& chown -R murmur:murmur /opt/murmur \  
&& rm -rf /tmp/* /var/tmp/*  
  
EXPOSE 64738/tcp 64738/udp  
  
VOLUME
["/opt/murmur/cert","/opt/murmur/config","/opt/murmur/data","/opt/murmur/log"]  
  
ENTRYPOINT ["docker-entrypoint.sh"]  
  
CMD ["murmur"]  

