# Builds production image for rumors-api.  
# Environments not included, should be composed in
https://github.com/MrOrz/rumors-deploy.  
#  
FROM kkarczmarczyk/node-yarn:6.9  
WORKDIR /srv/www  
  
# make node_modules cached.  
# Src: https://nodesource.com/blog/8-protips-to-start-killing-it-when-
dockerizing-node-js/  
#  
COPY package.json yarn.lock ./  
  
# When running with --production --pure-lockfile,  
# There will always be some missing modules. Dunno why...  
#  
RUN yarn  
  
# Other files, so that other files do not interfere with node_modules cache  
#  
COPY . .  
  
EXPOSE 5000  
ENTRYPOINT NODE_ENV=production ELASTIC_LOG_LEVEL=info npm start  

