FROM ubuntu:latest

ENV EDITOR vim
ENV SHELL bash

RUN apt-get -q update && \
    apt-get install --no-install-recommends -y --force-yes -q \
	autoconf \
	automake \
	make     \
	gcc      \
	libc-bin \
	libtool  \
	g++ 	 \
	libdb++-dev  \	
	libdb-dev  \
	openssl  \
	libssl-dev  \
	libevent-dev \
	bsdmainutils \
	git \
	libboost-all-dev \
	libevent-dev \
	libgnutls-dev \
	openssl \
	curl \
	wget \
	ca-certificates


RUN git clone https://github.com/bitcoin/bitcoin.git  ~/bitcoin && cd ~/bitcoin && git checkout -b v0.15.1 tags/v0.15.1
RUN cd ~/bitcoin && ./autogen.sh && ./configure --with-incompatible-bdb && make && make install && make clean
RUN rm -rf ~/bitcoin 
