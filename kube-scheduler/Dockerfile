FROM quay.io/liamleane/kube-master:latest

ENV container=docker
ENV NAME=kube-scheduler VERSION=0.1 RELEASE=8 ARCH=x86_64

LABEL name="kube-scheduler"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"
LABEL RUN /usr/bin/docker run -d --net=host

ADD launch.sh /usr/bin/kube-scheduler-docker.sh

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/etc/kubernetes && cp /etc/kubernetes/{config,scheduler} /exports/hostfs/etc/kubernetes

ENTRYPOINT ["/usr/bin/kube-scheduler-docker.sh"]
