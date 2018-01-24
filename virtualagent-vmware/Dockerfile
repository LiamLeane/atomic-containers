FROM registry.fedoraproject.org/fedora:27

LABEL Name="vmware"
LABEL Version="0.1"
LABEL atomic.type='system'
LABEL Architecture="x86_64"

ADD exports/service.template /exports/

RUN dnf -y --setopt=tsflags=nodocs install open-vm-tools && dnf clean all