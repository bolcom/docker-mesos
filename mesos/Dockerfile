FROM ubuntu
MAINTAINER RedJack, LLC

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

# Make sure to install OpenJDK 6 explicitly.  The libmesos library includes an
# RPATH entry, which is needed to find libjvm.so at runtime.  This RPATH is
# hard-coded to the OpenJDK version that was present when the package was
# compiled.  So even though the Debian package claims that it works with either
# OpenJDK 6 or OpenJDK 7, the fact that Mesosphere compiled with OpenJDK 6 means
# that we have to have that specific version present at runtime.

WORKDIR /tmp
RUN \
  apt-get install -y curl openjdk-6-jre-headless && \
  curl -s -o mesos.deb https://downloads.mesosphere.io/master/ubuntu/14.04/mesos_0.21.0-1.0.ubuntu1404_amd64.deb && \
  dpkg --unpack mesos.deb && \
  apt-get install -f -y && \
  rm mesos.deb && \
  apt-get clean
