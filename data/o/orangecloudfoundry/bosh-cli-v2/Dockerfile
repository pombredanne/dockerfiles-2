FROM ubuntu:16.04  
ENV BOSH_CLI_VERSION 3.0.1  
ENV BOSH_CLI_SUM ccc893bab8b219e9e4a628ed044ebca6c6de9ca0  
ENV BOSH_CLI_FILENAME bosh-cli-${BOSH_CLI_VERSION}-linux-amd64  
  
ENV DEBIAN_PACKAGES "ca-certificates wget git openssh-client file"  
# https://bosh.io/docs/cli-env-deps.html  
ENV BOSH_ENV_DEPS "build-essential zlibc zlib1g-dev ruby ruby-dev openssl
libxslt-dev \  
libxml2-dev libssl-dev libreadline6 libreadline6-dev libyaml-dev
libsqlite3-dev sqlite3"  
ENV BOSH_AWS_CPI_URL https://bosh.io/d/github.com/cloudfoundry-incubator/bosh-
aws-cpi-release?v=69  
ENV BOSH_AWS_CPI_CHECKSUM 8abe70219244896ea6f7208fc01f2eac56179170  
  
RUN apt-get update \  
&& apt-get -y upgrade \  
&& apt-get install -y --no-install-recommends ${DEBIAN_PACKAGES} \  
&& apt-get install -y --no-install-recommends ${BOSH_ENV_DEPS} \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN wget -nv https://s3.amazonaws.com/bosh-cli-artifacts/${BOSH_CLI_FILENAME}
\  
&& echo "${BOSH_CLI_SUM} ${BOSH_CLI_FILENAME}" | sha1sum -c - \  
&& chmod +x ${BOSH_CLI_FILENAME} \  
&& mv ${BOSH_CLI_FILENAME} /usr/local/bin/bosh  
  
COPY bosh_init_cache /tmp/bosh_init_cache/  
RUN /tmp/bosh_init_cache/seed_bosh_init_cache.sh && \  
rm -rf /tmp/bosh_init_cache  

