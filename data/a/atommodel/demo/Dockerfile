# Pull base image.  
FROM phusion/baseimage  
  
MAINTAINER Michael Chin  
  
# Use baseimage-docker's init system.  
CMD ["/sbin/my_init"]  
  
RUN apt-get update -y  
  
RUN apt-get install -y git python-pip cython clang libnetcdf-dev python-
mpltoolkits.basemap python-numpy python-scipy python-h5py  
  
RUN pip install -U setuptools  
RUN pip install -U pip  
RUN pip install jupyter  
RUN pip install netcdf4  
RUN pip install colorlover  
  
RUN apt-get update -y  
RUN apt-get install -y gmt wget  
RUN apt-get install -y libglew-dev  
RUN apt-get install -y python2.7-dev  
RUN apt-get install -y libboost-dev libboost-python-dev libboost-thread-dev
libboost-program-options-dev libboost-test-dev libboost-system-dev  
RUN apt-get install -y libqt4-dev  
RUN apt-get install -y libgdal1-dev  
RUN apt-get install -y libcgal-dev  
RUN apt-get install -y libproj-dev  
RUN apt-get install -y libqwt-dev  
RUN apt-get install -y libxrender-dev libice-dev libsm-dev libfreetype6-dev
libfontconfig1-dev  
  
RUN wget --content-disposition -c
https://sourceforge.net/projects/gplates/files/pygplates/beta-
revision-12/pygplates-ubuntu-xenial_1.5_1_amd64.deb/download  
RUN dpkg -i pygplates-ubuntu-xenial_1.5_1_amd64.deb  
RUN apt-get -f install  
RUN cp /usr/lib/pygplates/revision12/pygplates.so /usr/lib/python2.7/dist-
packages/  
  
WORKDIR /build  
RUN git clone https://github.com/atom-model/ATOM.git  
WORKDIR /build/ATOM  
RUN make  
RUN pip install -e /build/ATOM/python  
  
RUN mkdir /workspace && \  
mkdir /workspace/volume  
  
# Copy test files to workspace  
RUN cp -av /build/ATOM/examples/* /workspace/  
  
# setup space for working in  
VOLUME /workspace/volume  
  
RUN mkdir /etc/service/notebook  
ADD notebook.sh /etc/service/notebook/run  
RUN chmod +x /etc/service/notebook/run  
  
# Clean up APT when done.  
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
EXPOSE 8888  

