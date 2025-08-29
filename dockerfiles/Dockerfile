FROM ghcr.io/taffish-org/python:3.13.2

LABEL maintainer="taffish@163.com"

USER root

WORKDIR /root

RUN apt-get update && apt-get install -y curl wget git gcc g++ make default-jdk && \
    pip install --upgrade pip pandas && \
    cd / && \
    curl -LO https://github.com/lh3/miniprot/releases/download/v0.18/miniprot-0.18.tar.bz2 && \
    tar xjf /miniprot-0.18.tar.bz2 && rm /miniprot-0.18.tar.bz2 && cd /miniprot-0.18/ && \
    make -j4 && PATH=/miniprot-0.18:${PATH} && \
    cd / && \
    wget http://eddylab.org/software/hmmer/hmmer.tar.gz && \
    tar zxf /hmmer.tar.gz && rm /hmmer.tar.gz && cd /hmmer-3.4/ && \
    ./configure --prefix /usr/local && make && make check && make install && \
    cd easel && make install && \
    cd / && \
    curl -LO https://github.com/smirarab/sepp/archive/refs/tags/v4.5.6.tar.gz && \
    tar -zxvf /v4.5.6.tar.gz && rm /v4.5.6.tar.gz && cd /sepp-4.5.6/ && \
    pip install . && config_sepp -c && \
    cd / && \
    curl -LO https://github.com/huangnengCSU/compleasm/archive/refs/tags/v0.2.7.tar.gz && \
    tar -zxvf /v0.2.7.tar.gz && rm /v0.2.7.tar.gz && cd /compleasm-0.2.7/ && \
    python setup.py install && \
    compleasm --help

ENV PATH=/miniprot-0.18:${PATH}

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=compleasm
