FROM fedora:rawhide
MAINTAINER [Martin Babinsky martbab@gmail.com]

RUN echo 'deltarpm = false' >> /etc/dnf/dnf.conf \
    && dnf update -y dnf \
    && dnf install -y dnf-plugins-core sudo wget \
    # FIXME: due to packaging issues the following is not a dependency of
    # python{2,3}-rpm-macros, and must be installed manually
    && dnf install -y python-srpm-macros \
    && dnf clean all

# install build dependencies from COPR and latest devel branch
RUN dnf install -y @buildsys-build @development-tools \
    && wget https://raw.githubusercontent.com/freeipa/freeipa/master/freeipa.spec.in \
    && dnf builddep -y --spec ./freeipa.spec.in \
        -D "with_lint 1" -D "with_wheels 1" --best --allowerasing \
    && dnf clean all \
    && rm -f ./freeipa.spec.in

# update everything and try to resolve conflicts
RUN dnf update -y --best --allowerasing && dnf clean all
