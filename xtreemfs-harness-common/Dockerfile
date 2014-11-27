FROM sequenceiq/pam:ubuntu-14.04
MAINTAINER Christoph Kleineweber <kleineweber@zib.de>

RUN apt-get -qy update && apt-get -qy install git make openjdk-7-jdk ant

RUN git clone https://github.com/xtreemfs/xtreemfs.git && \
    cd xtreemfs && \
    export XTREEMFS_SRC=`pwd` && \
    git checkout -b ckleineweber-QoS remotes/origin/ckleineweber-QoS && \
	make server
