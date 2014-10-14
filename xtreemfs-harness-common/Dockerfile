FROM ubuntu
MAINTAINER Christoph Kleineweber <kleineweber@zib.de>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qy update
RUN apt-get -qy dist-upgrade

RUN apt-get -qy install git make openjdk-7-jdk ant

RUN git clone https://github.com/xtreemfs/xtreemfs.git && \
    cd xtreemfs && \
    export XTREEMFS_SRC=`pwd` && \
    git checkout -b ckleineweber-QoS remotes/origin/ckleineweber-QoS && \
	make server
