FROM gwul/sfm-
base@sha256:07b3495d4496d603d464b3f829f92e61c6d27da8b773e1076e1b6ffcfd643eaf  
MAINTAINER Vict Tan <ychtan@email.gwu.edu>  
  
ADD . /opt/sfm-tumblr-harvester/  
WORKDIR /opt/sfm-tumblr-harvester  
RUN pip install -r requirements/common.txt -r requirements/release.txt  
  
ADD docker/exporter/invoke.sh /opt/sfm-setup/  
RUN chmod +x /opt/sfm-setup/invoke.sh  
  
CMD ["/opt/sfm-setup/invoke.sh"]  

