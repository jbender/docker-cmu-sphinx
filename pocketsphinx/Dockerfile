FROM jbender/sphinxbase:5prealpha
MAINTAINER Jonathan Bender <jlbender@gmail.com>

ENV POCKETSPHINX pocketsphinx-5prealpha

ADD ${POCKETSPHINX}.tar.gz /sphinx/

RUN mv /sphinx/${POCKETSPHINX} /sphinx/pocketsphinx

WORKDIR /sphinx/pocketsphinx

RUN \
./configure --with-swig-python && \
make && \
make check && \
make install && \
make installcheck

ENV LD_LIBRARY_PATH=/usr/local/lib
ENV PKG_CONFIG_PATH=/usr/local/lib/pkgconfig

WORKDIR /data

# 'make install' installs all python modules to this dir.
# But Ubuntu recognizes only /usr/local/lib/python3.4/dist-packages
# dir by default. So add this dir to PYTHON_PATH manually.
ENV PYTHONPATH /usr/local/lib/python3.4/site-packages

VOLUME /sphinx
VOLUME /data
