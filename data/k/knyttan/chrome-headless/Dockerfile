FROM debian:sid  
  
# Install deps + add Chrome Stable + purge all the things  
RUN apt-get update && apt-get install -y \  
apt-transport-https \  
ca-certificates \  
curl \  
gnupg \  
\--no-install-recommends \  
&& curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
\  
&& echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main"
> /etc/apt/sources.list.d/google-chrome.list \  
&& apt-get update && apt-get install -y \  
google-chrome-stable \  
\--no-install-recommends \  
&& apt-get purge --auto-remove -y curl gnupg \  
&& rm -rf /var/lib/apt/lists/*  
  
# Add Chrome as a user  
RUN groupadd -r chrome && useradd -r -g chrome -G audio,video chrome \  
&& mkdir -p /home/chrome && chown -R chrome:chrome /home/chrome  
  
USER root  
RUN apt-get update && apt-get install -y --no-install-recommends gosu  
COPY docker-entrypoint.sh /usr/local/bin/  
ENTRYPOINT ["docker-entrypoint.sh"]  
EXPOSE 9222  
CMD ["chrome-headless"]  

