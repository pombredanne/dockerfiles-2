FROM lsiobase/alpine.python:3.6  
# Set python to use utf-8 rather than ascii.  
ENV PYTHONIOENCODING="UTF-8"  
# Copy local files.  
COPY etc/ /etc  
RUN chmod -v +x \  
/etc/cont-init.d/* \  
/etc/services.d/*/run  
  
# Copy modular config  
ADD config /config  
RUN pip install yasha  
  
# Ports and volumes.  
EXPOSE 5050/tcp

