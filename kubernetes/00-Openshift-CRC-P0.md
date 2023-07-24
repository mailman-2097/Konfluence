# Introduction

https://www.redhat.com/sysadmin/codeready-containers

# Installation

```
wget https://mirror.openshift.com/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
tar xvf crc-linux-amd64.tar.xz
mv crc /usr/bin/

crc setup
crc start -p ~/crc-pull-secret.txt

grep -E 'svm|vmx' /proc/cpuinfo

```