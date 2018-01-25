FROM registry.fedoraproject.org/fedora:rawhide

ADD kubernetes.repo /etc/yum.repos.d/kubernetes.repo

RUN dnf clean all

LABEL name="kube-base"
LABEL version="1.0" 
LABEL architecture="x86_64" 
LABEL atomic.type="system"