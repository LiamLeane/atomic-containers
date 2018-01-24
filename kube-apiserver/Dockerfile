FROM appopsos.azurecr.io/kube-master:latest

ENV container=docker
ENV NAME=kube-apiserver VERSION=0.1 RELEASE=8 ARCH=x86_64

LABEL name="kube-apiserver"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"

ADD launch.sh /usr/bin/kube-apiserver-docker.sh

RUN chmod +x /usr/bin/kube-apiserver

LABEL RUN /usr/bin/docker/ run -d --net=host -p 443:443

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/usr/local/bin/ && cp /usr/bin/kubectl /exports/hostfs/usr/local/bin/kubectl

RUN mkdir -p /exports/hostfs/etc/kubernetes && cp /etc/kubernetes/{config,apiserver} /exports/hostfs/etc/kubernetes

ENTRYPOINT ["/usr/bin/kube-apiserver-docker.sh"]
