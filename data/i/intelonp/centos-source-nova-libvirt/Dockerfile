# Copyright (c) 2017, Intel Corporation  
#  
# Licensed under the Apache License, Version 2.0 (the "License");  
# you may not use this file except in compliance with the License.  
# You may obtain a copy of the License at  
#  
# http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
  
FROM intelonp/centos-source-base:0018  
MAINTAINER Intel Corp. (http://www.intel.com)  
  
  
  
  
  
  
  
  
RUN usermod --append --home /var/lib/nova \--groups kolla nova \  
&& usermod --append --groups qemu nova \  
&& mkdir -p /var/lib/nova \  
&& chown -R 42436:42436 /var/lib/nova  
  
  
  
  
  
  
  
  
RUN yum -y install libvirt-daemon libguestfs openvswitch qemu-kvm libvirt-
daemon-driver-nwfilter libvirt-daemon-config-nwfilter libvirt-daemon-driver-
lxc ceph-common && yum clean all  
  
  
  
COPY extend_start.sh /usr/local/bin/kolla_extend_start  
RUN chmod 755 /usr/local/bin/kolla_extend_start  
  
  

