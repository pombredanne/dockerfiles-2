# -- build environment --  
ARG PLUGIN_DIR=/opt/cni-plugins  
  
FROM golang:alpine AS build-env  
ARG PLUGIN_DIR  
RUN apk update && apk add git bash curl  
RUN mkdir -p $PLUGIN_DIR  
ENV CGO_ENABLED=0  
RUN git clone https://github.com/Intel-Corp/multus-cni.git && \  
cd multus-cni && ./build && cp bin/multus $PLUGIN_DIR && cd ..  
RUN curl -sL
https://github.com/containernetworking/plugins/releases/download/v0.7.0/cni-
plugins-amd64-v0.7.0.tgz | tar xzvC $PLUGIN_DIR  
  
# -- runtime container --  
FROM alpine:3.7  
ARG PLUGIN_DIR  
ENV PLUGIN_DIR=$PLUGIN_DIR  
ENV INSTALL_DIR=/opt/cni/bin/  
ENV CONF_DIR=/etc/cni/net.d/  
ENV CONF_TEMPLATE_DIR=/config/  
  
RUN apk update && apk add gettext  
  
RUN mkdir -p $CONF_TEMPLATE_DIR  
COPY \--from=build-env $PLUGIN_DIR/* $PLUGIN_DIR/  
COPY install.sh /  
ENTRYPOINT ["sh", "/install.sh"]  

