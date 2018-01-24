FROM registry.fedoraproject.org/fedora:27

LABEL Name="xenserver"
LABEL Version="0.1"
LABEL atomic.type='system'
LABEL Architecture="x86_64"

ADD nexus-virtualagents.repo /etc/yum.repos.d/nexus-virtualagents.repo

ADD exports/service.template /exports/

RUN dnf -y --setopt=tsflags=nodocs install xe-guest-utilities xe-guest-utilities-xenstore && dnf clean all

RUN rm -f /etc/yum.repos.d/nexus-virtualagents.repo