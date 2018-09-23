FROM ubuntu:latest

ENV EDITOR vim
ENV SHELL bash

RUN apt-get -q update && \
    apt-get install --no-install-recommends -y -q \
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
	openssl \
	curl \
	wget \
	ca-certificates


RUN git clone https://github.com/bitcoin/bitcoin.git  ~/bitcoin && cd ~/bitcoin && git checkout -b v0.16.3 tags/v0.16.3
RUN cd ~/bitcoin && ./autogen.sh && ./configure --with-incompatible-bdb && make && make install && make clean
RUN rm -rf ~/bitcoin 


#RUN useradd -s /bin/bash -m /var/lib/btc btc
RUN mkdir -p /var/lib/btc && useradd -s /bin/bash -d /var/lib/btc btc
RUN chown btc:btc -R /var/lib/btc

#Copy the script over to the image
COPY btc.sh /var/lib/btc/
RUN chown btc /var/lib/btc/btc.sh && chgrp btc /var/lib/btc/btc.sh && chmod u+x /var/lib/btc/btc.sh


#Volume
VOLUME ["/var/lib/btc"]

# node service
EXPOSE 8333

# RPC service
EXPOSE 8332

USER btc

#cmd to exeucute 
#CMD ["bitcoind"]
ENTRYPOINT ["/var/lib/btc/btc.sh"]
