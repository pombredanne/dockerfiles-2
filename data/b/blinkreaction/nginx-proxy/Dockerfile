FROM alpine:3.4  
MAINTAINER Leonid Makarov <leonid.makarov@blinkreaction.com>  
  
RUN apk add --update --no-cache \  
curl \  
supervisor \  
openssl \  
nginx \  
&& rm -rf /var/cache/apk/*  
  
# Install docker-gen  
ENV DOCKER_GEN_VERSION 0.7.3  
ENV DOCKER_GEN_TARFILE docker-gen-alpine-linux-
amd64-$DOCKER_GEN_VERSION.tar.gz  
RUN curl -sSL https://github.com/jwilder/docker-
gen/releases/download/$DOCKER_GEN_VERSION/$DOCKER_GEN_TARFILE -O && \  
tar -C /usr/local/bin -xvzf $DOCKER_GEN_TARFILE && \  
rm $DOCKER_GEN_TARFILE  
  
RUN chown -R nginx:nginx /var/lib/nginx  
  
# Generate SSL certificate and key  
RUN openssl req -batch -nodes -newkey rsa:2048 -keyout /etc/nginx/server.key
-out /tmp/server.csr && \  
openssl x509 -req -days 365 -in /tmp/server.csr -signkey /etc/nginx/server.key
-out /etc/nginx/server.crt; rm /tmp/server.csr  
  
COPY conf/nginx.conf /etc/nginx/nginx.conf  
COPY conf/nginx.default.conf.tmpl /etc/nginx/default.conf.tmpl  
COPY conf/supervisord.conf /etc/supervisor.d/docker-gen.ini  
  
CMD ["supervisord", "-n"]  

