FROM registry.fedoraproject.org/fedora:27

LABEL Name="hyperv"
LABEL Version="0.1"
LABEL atomic.type='system'
LABEL Architecture="x86_64"

ADD openlogic-microsoft.repo /etc/yum.repos.d/openlogic-microsoft.repo

RUN dnf -y --setopt=tsflags=nodocs install kmod-microsoft-hyper-v microsoft-hyper-v && dnf clean all
ADD exports/service.template /exports/

