FROM pipill/armhf-alpine:3.4  
RUN [ "cross-build-start" ]  
  
RUN apk --update upgrade \  
&& apk --no-cache --no-progress add ca-certificates \  
&& rm -rf /var/cache/apk/*  
  
RUN [ "cross-build-end" ]  
  
COPY traefik /usr/local/bin/  
COPY entrypoint.sh /  
EXPOSE 80  
ENTRYPOINT ["/entrypoint.sh"]  
CMD ["--help"]  
  
# Metadata  
LABEL org.label-schema.vendor="Containous" \  
org.label-schema.url="https://traefik.io" \  
org.label-schema.name="Traefik" \  
org.label-schema.description="A modern reverse-proxy" \  
org.label-schema.version="v1.3.1" \  
org.label-schema.docker.schema-version="1.0"  

