FROM amazeeio/nginx-drupal  
  
ENV WEBROOT=docroot  
  
COPY docker/drupal.conf /etc/nginx/conf.d/app.conf  
RUN fix-permissions /etc/nginx  
  

