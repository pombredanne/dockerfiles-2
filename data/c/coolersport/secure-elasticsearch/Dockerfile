FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.3  
COPY entrypoint.sh /  
  
RUN yum update -y && yum upgrade -y && yum install -y openssl && \  
/usr/share/elasticsearch/bin/elasticsearch-plugin install -b
com.floragunn:search-guard-6:6.2.3-22.0 && \  
chmod u+x /usr/share/elasticsearch/plugins/search-guard-6/tools/*.sh && \  
chown -R elasticsearch /usr/share/elasticsearch/plugins/search-guard-6 && \  
chmod u+x /entrypoint.sh && \  
yum clean all && rm -rf /var/cache/yum  
  
ENTRYPOINT ["/entrypoint.sh"]  
CMD ["eswrapper"]  

