FROM limaofeng/node-alpine:latest  
MAINTAINER limaofeng <limaofeng@msn.com>  
  
RUN npm install pm2@next -g  
  
VOLUME ["/app"]  
  
# Expose ports  
EXPOSE 80 443 43554  
WORKDIR /app  
  
# Start process.yml  
CMD ["pm2-docker", "start", "--auto-exit", "--env", "production",
"process.yml"]  

