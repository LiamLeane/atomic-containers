FROM appopsos.azurecr.io/kube-node:latest

LABEL name="kube-proxy"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"
LABEL RUN /usr/bin/docker run -d --privileged --net=host 

ENV container=docker
ENV NAME=kube-proxy VERSION=0 RELEASE=8 ARCH=x86_64

RUN dnf install -y --setopt=tsflags=nodocs iptables conntrack-tools && dnf clean all

ADD launch.sh /usr/bin/kube-proxy-docker.sh

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/etc/kubernetes && cp /etc/kubernetes/{config,proxy} /exports/hostfs/etc/kubernetes

ENTRYPOINT ["/usr/bin/kube-proxy-docker.sh"]

