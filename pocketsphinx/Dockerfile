FROM jbender/sphinxbase:5prealpha
MAINTAINER Jonathan Bender <jlbender@gmail.com>

ENV POCKETSPHINX pocketsphinx-5prealpha

ADD ${POCKETSPHINX}.tar.gz /sphinx/

RUN mv /sphinx/${POCKETSPHINX} /sphinx/pocketsphinx

WORKDIR /sphinx/pocketsphinx

RUN echo "==> Updating and installing packages" && \
    apt-get update && \
    apt-get install -y build-essential gcc automake autoconf libtool && \
    echo "==> Installing Sphinx" && \
    ./configure --with-swig-python && \
    make && \
    make check && \
    make install && \
    echo "==> Verifying Install" && \
    make installcheck && \
    echo "==> Cleaning Up" && \
    rm -rf /var/lib/{apt,dpkg,cache,log} && \
    apt-get remove -y --auto-remove build-essential gcc automake autoconf libtool && \
    apt-get clean

ENV LD_LIBRARY_PATH=/usr/local/lib
ENV PKG_CONFIG_PATH=/usr/local/lib/pkgconfig

WORKDIR /data

# 'make install' installs all python modules to this dir.
# But Ubuntu recognizes only /usr/local/lib/python3.4/dist-packages
# dir by default. So add this dir to PYTHON_PATH manually.
ENV PYTHONPATH /usr/local/lib/python3.4/site-packages

VOLUME /sphinx
VOLUME /data
