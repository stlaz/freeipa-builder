# FreeIPA Builder

repository of FreeIPA docker builder images
===========================================

This repo contains Dockerfiles for creating a containerized environment for
building FreeIPA packages. It currently only containers optimized for building
freeipa master on latest and rawhide Fedora, but more images will be coming
soon.

You can create an image and run the build in your repo (assuming you have
docker up and running) like this:

```
# build the Fedora latest image first
docker build -t freeipa-builder:master:fedora:latest \
    https://github.com/martbab/freeipa-builder.git#master:fedora/latest

# clone FreeIPA repo
git clone https://github.com/freeipa/freeipa.git && cd freeipa

# build the RPMs while preserving the correct ownership of the built artifacts
docker run -v $PWD:/freeipa -w /freeipa \
    /bin/bash -c "make rpms && chown -R $UID:$GROUPS dist" 
```
