FROM node:6-alpine  
  
# update package index and install git  
RUN apk add --update --no-cache git  
  
WORKDIR /app  
  
COPY package.json /app/  
  
RUN npm install --quiet  
  
COPY . /app/  
  
RUN npm run linebreak-check  
RUN npm run build  
  
CMD /bin/ash  

