FROM ubuntu:latest  
MAINTAINER Nathan Craike <ncraike@gmail.com>  
  
RUN apt-get update  
  
RUN apt-get -y install \  
curl \  
build-essential \  
git \  
pandoc  
  
# Install node.js  
RUN curl -sL https://deb.nodesource.com/setup | bash -  
RUN apt-get -y install nodejs  
  
# Install grunt  
RUN npm install -g grunt-cli  
  
# Install reveal.js  
RUN git clone https://github.com/hakimel/reveal.js.git  
RUN cd reveal.js; npm install  
  
COPY index.html /slides/  
RUN rm /reveal.js/index.html  
RUN ln -s /slides/index.html /reveal.js/index.html  
  
COPY Gruntfile.js /reveal.js/  
  
# Pandoc search for...  
# http://localhost:8000/reveal.js/css/reveal.min.css  
# http://localhost:8000/reveal.js/js/reveal.min.js  
# http://localhost:8000/reveal.js/lib/js/head.min.js  
# http://localhost:8000/reveal.js/css/print/pdf.css  
# http://localhost:8000/reveal.js/css/theme/simple.css  
# http://localhost:35729/livereload.js?snipver=1  
# http://localhost:8000/reveal.js/css/theme/simple.css  
# http://localhost:8000/reveal.js/css/print/pdf.css  
# http://localhost:8000/reveal.js/plugin/zoom-js  
RUN mkdir -p /pandoc/reveal.js/css/lib  
RUN mkdir -p /pandoc/reveal.js/js  
RUN mkdir -p /pandoc/reveal.js/lib/js  
RUN mkdir -p /pandoc/reveal.js/css/print  
RUN ["ln", "-s", "/reveal.js/css/reveal.css",
"/pandoc/reveal.js/css/reveal.min.css"]  
RUN ["ln", "-s", "/reveal.js/js/reveal.js" ,
"/pandoc/reveal.js/js/reveal.min.js"]  
RUN ["ln", "-s", "/reveal.js/lib/js/head.min.js",
"/pandoc/reveal.js/lib/js/head.min.js"]  
RUN ["ln", "-s", "/reveal.js/css/print/pdf.css",
"/pandoc/reveal.js/css/print/pdf.css"]  
RUN ["ln", "-s", "/reveal.js/css/theme/", "/pandoc/reveal.js/css/theme"]  
RUN ["ln", "-s", "/reveal.js/plugin", "/pandoc/reveal.js/plugin"]  
  
WORKDIR reveal.js  
CMD grunt serve  
EXPOSE 8000  

