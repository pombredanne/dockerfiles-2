FROM amazeeio/centos7-mariadb10-drupal  
  
USER root  
COPY docker/server.cnf /etc/my.cnf.d/server.cnf  
RUN fix-permissions /etc/my.cnf.d/  
  
USER mysql  

