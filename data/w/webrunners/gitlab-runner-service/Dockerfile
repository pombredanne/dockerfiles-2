FROM gitlab/gitlab-runner:latest  
  
ENV TERM=linux TZ=Europe/Berlin  
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone  
  
ENV DOCKER_FILE=docker-17.12.1-ce.tgz
DOCKER_URL=https://download.docker.com/linux/static/stable/x86_64  
RUN apt-get update -yq && apt-get dist-upgrade -yq && apt-get install -yq
--no-install-recommends curl ca-certificates\  
&& curl -fsSLO $DOCKER_URL/$DOCKER_FILE\  
&& tar xzvf $DOCKER_FILE\  
&& mv docker/docker /usr/local/bin\  
&& chmod a+x /usr/local/bin/docker\  
&& rm -r docker $DOCKER_FILE\  
&& curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-
compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose\  
&& chmod +x /usr/local/bin/docker-compose\  
&& apt-get -yqq clean &&\  
apt-get -yqq autoclean &&\  
apt-get -yqq autoremove &&\  
rm -rf /var/lib/apt/* &&\  
rm -rf /var/lib/cache/* &&\  
rm -rf /var/lib/log/* &&\  
rm -rf /var/tmp/* &&\  
rm -rf /tmp/*  
  
COPY ./context/runner-init.sh /  
RUN chmod a+x /runner-init.sh  
  
ENTRYPOINT ["/usr/bin/dumb-init", "/runner-init.sh"]  
  
CMD ["run", "--user=gitlab-runner", "--working-directory=/home/gitlab-runner"]  

