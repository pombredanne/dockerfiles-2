FROM russellcloud/python-base:latest-py3  
MAINTAINER RussellCloud Team "support@russellcloud.cn"  
# Install some dependencies  
RUN apt-get update && apt-get install -y \  
ant \  
apt-utils \  
bc \  
build-essential \  
cmake \  
default-jdk \  
doxygen \  
gfortran \  
libeigen3-dev \  
libfreetype6-dev \  
libhdf5-dev \  
liblcms2-dev \  
libopenblas-dev \  
liblapack-dev \  
libpng12-dev \  
libpython3-dev \  
libtiff-dev \  
libtiff5-dev \  
libzmq3-dev \  
nano \  
pkg-config \  
python3-dev \  
python3-tk \  
rsync \  
software-properties-common \  
unzip \  
vim \  
webp \  
&& \  
apt-get clean && \  
apt-get autoremove && \  
rm -rf /var/lib/apt/lists/* && \  
# Link BLAS library to use OpenBLAS using the alternatives mechanism
(https://www.scipy.org/scipylib/building/linux.html#debian-ubuntu)  
update-alternatives --set libblas.so.3 /usr/lib/openblas-base/libblas.so.3

