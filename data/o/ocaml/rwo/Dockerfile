FROM ocaml/opam:ubuntu-16.04_ocaml-4.06.0  
RUN sudo apt-get update && sudo apt-get -y install python-pygments tzdata  
RUN opam repo set-url default https://opam.ocaml.org/  
ENV OPAMYES=1  
ENV OPAMJOBS=3  
WORKDIR /home/opam/src  
  
# update opam  
RUN opam update  
  
# pre-install dependencies  
RUN opam depext -iy core async ppx_sexp_conv ppx_deriving jbuilder \  
toplevel_expect_test patdiff lambdasoup sexp_pretty fmt re  
# Required for code blocks  
# core_bench mtime yojson astring cryptokit ocp-index atd atdgen ctypes \  
# ctypes-foreign textwrap uri  
# cohttp-async  
#install pandoc  
WORKDIR /tmp  
RUN curl -OL
https://github.com/jgm/pandoc/releases/download/2.1.3/pandoc-2.1.3-1-amd64.deb
&& sudo dpkg -i pandoc-2.1.3-1-amd64.deb  
WORKDIR /home/opam/src  
  
# compile the project  
COPY . /home/opam/src/  
RUN sudo chown -R opam /home/opam/src  
RUN opam config exec \-- make  

