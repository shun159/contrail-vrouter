contrail-vrouter
================

Contrail Virtual Router

The Contrail Virtual Router implements the data-plane functionality that allows a virtual interface to be associated
with a [VRF](http://en.wikipedia.org/wiki/Virtual_Routing_and_Forwarding).

The Contrail Virtual Router is distributed under the terms of the BSD 2-Clause License and the GPLv2.

The implementation is split into a generic "dp-core" directory used by
multiple operating systems and OS-specific glue. The "linux" directory
contains the Linux specific code.

The code has been tested with both 2.6.32 and 3.0 kernel series and
with both KVM and Xen as hypervisors.

The utils directory contains user space applications that can be used
to created interfaces (utils/vif) or display the state of the kernel
module.

building vrouter.ko for a specific OS
==================================

```shellsession
$ apt install -y libboost-all-dev libnl-genl-3-dev libxml2-dev \
    liburcu-dev byacc flex libpcap-dev scons python python-pip \
    pkg-config zlib1g-dev libglib2.0-dev libfdt-dev libpixman-1-dev \
    cloud-image-utils
$ wget http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/libu/liburcu/liburcu2_0.8.5-1ubuntu1~cloud0_amd64.deb
$ wget http://ubuntu-cloud.archive.canonical.com/ubuntu/pool/main/libu/liburcu/liburcu-dev_0.8.5-1ubuntu1~cloud0_amd64.deb
$ sudo dpkg -i liburcu2_0.8.5-1ubuntu1~cloud0_amd64.deb
$ sudo dpkg -i liburcu-dev_0.8.5-1ubuntu1~cloud0_amd64.deb
$ git clone https://github.com/Juniper/contrail-vrouter vrouter
$ git clone https://github.com/Juniper/contrail-build tools/build
$ git clone https://github.com/Juniper/contrail-sandesh tools/sandesh
$ git clone https://github.com/Juniper/contrail-common src/contrail-common
$ scons vrouter -j2 --kernel-dir=/lib/modules/5.0.0-37-generic/build/ --without-dpdk --add-opts=-std=c99
$ cd vrouter; sudo insmod vrouter.ko
```
