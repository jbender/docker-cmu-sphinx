FROM jbender/sphinxbase:5prealpha
MAINTAINER Jonathan Bender <jlbender@gmail.com>

ENV SPHINXTRAIN sphinxtrain-5prealpha

ADD ${SPHINXTRAIN}.tar.gz /sphinx/

RUN mv /sphinx/${SPHINXTRAIN} /sphinx/sphinxtrain

WORKDIR /sphinx/sphinxtrain

RUN \
./configure && \
make && \
make check && \
make installcheck

WORKDIR /data

# 'make install' installs all python modules to this dir.
# But Ubuntu recognizes only /usr/local/lib/python3.4/dist-packages
# dir by default. So add this dir to PYTHON_PATH manually.
ENV PYTHONPATH /usr/local/lib/python3.4/site-packages

VOLUME /sphinx
VOLUME /data
