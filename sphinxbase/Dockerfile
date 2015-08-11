FROM debian:8
MAINTAINER Jonathan Bender <jlbender@gmail.com>

ENV SPHINXBASE sphinxbase-5prealpha

ADD ${SPHINXBASE}.tar.gz /sphinx/

RUN mv /sphinx/${SPHINXBASE} /sphinx/sphinxbase

RUN echo "==> Updating and installing packages" && \
    apt-get update && \
    apt-get install -y build-essential gcc automake autoconf libtool && \
    apt-get install -y swig python3-dev python3-numpy python3-scipy && \
    apt-get install -y sox bison && \
    echo "==> Installing Sphinx" && \
    cd /sphinx/sphinxbase && \
    ./autogen.sh && \
    ./configure --with-swig-python && \
    make && \
    make install && \
    echo "==> Cleaning Up" && \
    rm -rf /var/lib/{apt,dpkg,cache,log} && \
    apt-get remove -y --auto-remove build-essential gcc automake autoconf libtool && \
    apt-get clean

WORKDIR /sphinx/sphinxbase
