FROM appopsos.azurecr.io/virtualagent-hyperv:latest

LABEL Name="azure"
LABEL Version="0.1"
LABEL atomic.type='system'
LABEL Architecture="x86_64"

RUN dnf -y --setopt=tsflags=nodocs install WALinuxAgent && dnf clean all

ADD exports/service.template /exports/

