FROM neo4j  
LABEL maintainer="Syed Hassaan Ahmed"  
  
ADD
https://gist.githubusercontent.com/jexp/1e295d5f5b96e8e42fb614232abdbb4f/raw/ee277d2daec8aa54c031cbeede774abda9c9118b/neo4j-wait.sh
./  
ADD
https://gist.githubusercontent.com/syedhassaanahmed/1809fcce4cb15daaff79690932ea76bd/raw/6f660641eccf662936b13cf077465fbf9a46c1d2/neo4j-import.sh
./import.sh  
ADD https://raw.githubusercontent.com/neo4j-examples/game-of-
thrones/master/got-import.cypher ./import.cypher  
ADD https://github.com/neo4j-contrib/neo4j-apoc-
procedures/releases/download/3.3.0.1/apoc-3.3.0.1-all.jar ./plugins  
  
RUN chmod +x *.sh && apk add --update curl && rm -rf /var/cache/apk/*  
  
CMD ["./import.sh"]

