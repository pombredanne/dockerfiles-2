FROM parity/parity:v1.9.7  
# install all dependencies  
RUN apt-get update \  
&& apt-get install --yes --no-install-recommends curl \  
&& rm -rf /var/lib/apt/lists/*  
  
WORKDIR /  
COPY dev-key.json /parity/keys/InstantSealChain/dev-key.json  
COPY instant-seal-chain-spec.json /parity/instant-seal-chain-spec.json  
COPY instant-seal-config.toml /parity/instant-seal-config.toml  
COPY ./common_start.sh /common_start.sh  
COPY start.sh /start.sh  
RUN echo "" > /parity/password  
RUN chmod +x /start.sh  
  
ENTRYPOINT [ "/start.sh" ]  
  
# docker image build --tag parity-dev-node .  
# docker container run --rm -it -p 8000:8000 -p 8001:8001 -p 8545:8545 -p
8180:8180 --name parity-dev-node parity-dev-node  

