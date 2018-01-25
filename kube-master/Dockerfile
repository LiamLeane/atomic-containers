FROM quay.io/liamleane/kube-base:latest

ENV NAME=kube-master VERSION=0 RELEASE=0 ARCH=x86_64

LABEL name="kube-master"
LABEL version="1.0" 
LABEL architecture="x86_64"

RUN dnf -y --setopt=tsflags=nodocs update && dnf clean all

RUN groupadd -g 994 kube && useradd -u 996 -g 994 kube

RUN dnf install -y kubernetes-master findutils && dnf clean all
