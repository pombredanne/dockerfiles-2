FROM yobasystems/alpine:amd64  
LABEL maintainer "Dominic Taylor <dominic@yobasystems.co.uk>"
architecture="AMD64/x86_64" version="10.6.0"  
  
RUN apk add --update \  
bash \  
ca-certificates \  
git \  
openssl \  
wget  
  
RUN wget -O /usr/bin/gitlab-ci-multi-runner https://gitlab-runner-
downloads.s3.amazonaws.com/v10.6.0/binaries/gitlab-runner-linux-amd64 && \  
chmod +x /usr/bin/gitlab-ci-multi-runner && \  
ln -s /usr/bin/gitlab-ci-multi-runner /usr/bin/gitlab-runner && \  
wget -q https://github.com/docker/machine/releases/download/v0.12.0/docker-
machine-Linux-x86_64 -O /usr/bin/docker-machine && \  
chmod +x /usr/bin/docker-machine && \  
mkdir -p /etc/gitlab-runner/certs && \  
chmod -R 700 /etc/gitlab-runner  
  
ADD files/entrypoint.sh /  
RUN chmod +x /entrypoint.sh  
  
VOLUME ["/etc/gitlab-runner", "/home/gitlab-runner"]  
ENTRYPOINT ["/entrypoint.sh"]  
CMD ["run", "--user=gitlab-runner", "--working-directory=/home/gitlab-runner"]  

