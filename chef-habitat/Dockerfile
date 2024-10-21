FROM busybox

ARG CHANNEL="stable"
ARG HAB_VERSION="1.6.1041"
ARG HABITAT_PACKAGE="core/hab/1.6.1041"

ARG INFRA_CHANNEL="unstable"
ARG INFRA_PACKAGE="ashiqueps/chef-infra-client"
ARG INFRA_PACKAGE_VERSION="19.0.35"

ADD https://packages.chef.io/files/${CHANNEL}/habitat/${HAB_VERSION}/hab-x86_64-linux.tar.gz /tmp/hab.tar.gz

RUN mkdir /tmp/hab
RUN tar -xzf /tmp/hab.tar.gz -C /tmp/hab && \
    cd /tmp/hab && \
    HAB_DIR=$(find . -type d -name "hab-*") && \
    cp $HAB_DIR/hab /tmp/hab/hab 

ENV HAB_LICENSE="accept-no-persist"
RUN /tmp/hab/hab pkg install --binlink --force --channel "${CHANNEL}" "${HABITAT_PACKAGE}"
RUN cp /tmp/hab/hab /hab/hab_bin
RUN rm /tmp/hab.tar.gz
RUN rm -rf /tmp/hab

RUN hab pkg install --channel "${CHANNEL}" "core/bash"
RUN TMP=$(hab pkg path core/bash) && ln -s "${TMP}/bin/bash" /bin/bash

RUN hab pkg install --binlink --force --channel "${INFRA_CHANNEL}" "${INFRA_PACKAGE}"

VOLUME [ "/hab" ]
