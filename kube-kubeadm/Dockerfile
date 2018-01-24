FROM appopsos.azurecr.io/kube-base:latest

ENV NAME=kube-kubeadm VERSION=0 RELEASE=0 ARCH=x86_64

LABEL name="kube-kubeadm"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"
LABEL RUN /usr/bin/docker run -d --privileged --net=host --pid=host -v /:/rootfs:ro -v /sys:/sys:rw -v /var/run:/var/run:rw -v /run:/run:rw -v /var/lib/docker:/var/lib/docker:rw -v /var/lib/kubelet:/var/lib/kubelet:slave -v /var/log/containers:/var/log/containers:rw

RUN dnf install -y --setopt=tsflags=nodocs docker iproute kubernetes-kubeadm kubernetes-node kubernetes-client containernetworking-cni ethtool ebtables && dnf clean all

ADD launch.sh /usr/bin/

ADD exports/service.template /exports/

ADD exports/config.json.template /exports/

RUN mkdir -p /exports/hostfs/usr/local/bin/ && cp /usr/bin/{kubectl,kubeadm} /exports/hostfs/usr/local/bin/
RUN mkdir -p /exports/hostfs/etc/{kubernetes,cni}
RUN mkdir -p /exports/hostfs/etc/kubernetes/pki
RUN mkdir -p /var/lib/kubelet

RUN cat /etc/systemd/system/kubelet.service.d/kubeadm.conf | grep Environment | sed 's/Environment="//g' | sed 's/\=/\=\"/' > /exports/hostfs/etc/kubernetes/kubeadm-env

ENTRYPOINT ["/usr/bin/launch.sh"]