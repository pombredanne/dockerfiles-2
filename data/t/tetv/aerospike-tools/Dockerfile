#  
# Aerospike Tools Dockerfile  
#  
# http://github.com/aerospike/aerospike-tools.docker  
#  
FROM ubuntu:xenial  
  
ENV AEROSPIKE_VERSION 3.15.3.2  
ENV AEROSPIKE_SHA256
e544d94728a85a19bc3f671fb50b1073bdd2f239573180269303e2487ee93c48  
  
# Work from /aerospike  
WORKDIR /aerospike  
  
ENV PATH /aerospike:$PATH  
  
# Install Aerospike  
RUN \  
apt-get update -y \  
&& apt-get install -y python wget logrotate ca-certificates python-dev python-
setuptools python-argparse python-bcrypt openssl python-openssl \  
&& wget "https://www.aerospike.com/artifacts/aerospike-
tools/${AEROSPIKE_VERSION}/aerospike-
tools-${AEROSPIKE_VERSION}-ubuntu16.04.tgz" -O aerospike-tools.tgz \  
&& echo "$AEROSPIKE_SHA256 *aerospike-tools.tgz" | sha256sum -c - \  
&& mkdir aerospike \  
&& tar xzf aerospike-tools.tgz --strip-components=1 -C aerospike \  
&& apt-get purge -y --auto-remove wget ca-certificates  
  
RUN ls /aerospike/aerospike && dpkg -i /aerospike/aerospike/aerospike-
tools-*.ubuntu16.04.x86_64.deb \  
&& rm -rf aerospike-tools.tgz aerospike /var/lib/apt/lists/*  
  
# Addition of wrapper script  
ADD wrapper.sh /aerospike/wrapper  
  
# Wrapper script entrypoint  
ENTRYPOINT ["wrapper"]  

