FROM appopsos.azurecr.io/kube-base:latest

ENV NAME=kube-node VERSION=0 RELEASE=0 ARCH=x86_64

LABEL name="kube-node"
LABEL version="1.0" 
LABEL architecture="x86_64"

RUN dnf -y --setopt=tsflags=nodocs update && dnf clean all

RUN dnf install -y --setopt=tsflags=nodocs kubernetes-node findutils && dnf clean all
