FROM quay.io/liamleane/kube-node:latest

ENV container=docker
ENV NAME=kube-kubelet VERSION=0 RELEASE=8 ARCH=x86_64

LABEL name="kube-kubelet"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"
LABEL RUN /usr/bin/docker run -d --privileged --net=host --pid=host -v /:/rootfs:ro -v /sys:/sys:rw -v /var/run:/var/run:rw -v /run:/run:rw -v /var/lib/docker:/var/lib/docker:rw -v /var/lib/kubelet:/var/lib/kubelet:slave -v /var/log/containers:/var/log/containers:rw

RUN dnf install -y --setopt=tsflags=nodocs util-linux ethtool systemd-udev e2fsprogs xfsprogs && dnf clean all

ADD launch.sh /usr/bin/kubelet-docker.sh

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/etc/kubernetes && cp /etc/kubernetes/{config,kubelet} /exports/hostfs/etc/kubernetes

ENTRYPOINT ["/usr/bin/kubelet-docker.sh"]
