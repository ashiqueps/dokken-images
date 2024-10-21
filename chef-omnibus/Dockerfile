FROM busybox
LABEL maintainer="Chef Software, Inc. <docker@chef.io>"

ARG CHANNEL=stable
ARG VERSION=18.5.0
ARG ARCH=x86_64
ARG PKG_VERSION=6

RUN wget "http://packages.chef.io/files/${CHANNEL}/chef/${VERSION}/el/${PKG_VERSION}/chef-${VERSION}-1.el${PKG_VERSION}.${ARCH}.rpm" -O /tmp/chef-client.rpm && \
    rpm2cpio /tmp/chef-client.rpm | cpio -idmv && \
    rm -rf /tmp/chef-client.rpm

VOLUME [ "/opt/chef" ]