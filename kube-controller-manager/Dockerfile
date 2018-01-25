FROM quay.io/liamleane/kube-master:latest

ENV container=docker
ENV NAME=kube-controller-manager VERSION=0.1 RELEASE=8 ARCH=x86_64

LABEL name="kube-controller-manager"
LABEL version="1.0"  
LABEL architecture="x86_64" 
LABEL atomic.type="system"

ADD launch.sh /usr/bin/kube-controller-manager-docker.sh

LABEL RUN /usr/bin/docker run -d --net=host

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/etc/kubernetes && cp /etc/kubernetes/{config,controller-manager} /exports/hostfs/etc/kubernetes

ENTRYPOINT ["/usr/bin/kube-controller-manager-docker.sh"]
