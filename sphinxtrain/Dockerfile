FROM jbender/sphinxbase:5prealpha
MAINTAINER Jonathan Bender <jlbender@gmail.com>

ENV SPHINXTRAIN sphinxtrain-5prealpha

ADD ${SPHINXTRAIN}.tar.gz /sphinx/

RUN mv /sphinx/${SPHINXTRAIN} /sphinx/sphinxtrain

WORKDIR /sphinx/sphinxtrain

RUN echo "==> Updating and installing packages" && \
    apt-get update && \
    apt-get install -y build-essential gcc automake autoconf libtool && \
    echo "==> Installing Sphinx" && \
    ./configure && \
    make && \
    make check && \
    echo "==> Verifying Install" && \
    make installcheck && \
    echo "==> Cleaning Up" && \
    rm -rf /var/lib/{apt,dpkg,cache,log} && \
    apt-get remove -y --auto-remove build-essential gcc automake autoconf libtool && \
    apt-get clean

WORKDIR /data

# 'make install' installs all python modules to this dir.
# But Ubuntu recognizes only /usr/local/lib/python3.4/dist-packages
# dir by default. So add this dir to PYTHON_PATH manually.
ENV PYTHONPATH /usr/local/lib/python3.4/site-packages

VOLUME /sphinx
VOLUME /data
