FROM debian:8
MAINTAINER Jonathan Bender <jlbender@gmail.com>

RUN \
apt-get update && \
apt-get install -y build-essential && \
apt-get install -y gcc automake autoconf libtool && \
apt-get install -y swig python3-dev python3-numpy python3-scipy && \
apt-get install -y sox bison

ENV SPHINXBASE sphinxbase-5prealpha

ADD ${SPHINXBASE}.tar.gz /sphinx/

RUN mv /sphinx/${SPHINXBASE} /sphinx/sphinxbase

WORKDIR /sphinx/sphinxbase
RUN \
./autogen.sh && \
./configure --with-swig-python && \
make && \
make install
