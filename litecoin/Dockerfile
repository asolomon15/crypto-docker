FROM ubuntu:xenial-20180808

ENV EDITOR vim
ENV SHELL bash


# setup to add bitcoin repository
RUN apt-get -q update && apt-get install software-properties-common --no-install-recommends -y -q && add-apt-repository ppa:bitcoin/bitcoin 

RUN apt-get -q update && \
    apt-get install --no-install-recommends -y  -q \
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


RUN git clone https://github.com/litecoin-project/litecoin.git  ~/litecoin && cd ~/litecoin && git checkout -b v0.16.3 tags/v0.16.3
RUN cd ~/litecoin && ./autogen.sh && ./configure --with-incompatible-bdb && make && make install && make clean
RUN rm -rf ~/litecoin


#RUN useradd -s /bin/bash -m /var/lib/ltc ltc
RUN mkdir -p /var/lib/ltc && useradd -s /bin/bash -d /var/lib/ltc ltc
RUN chown ltc:ltc -R /var/lib/ltc

#Copy the script over to the image
COPY ltc.sh /var/lib/ltc/
RUN chown ltc /var/lib/ltc/ltc.sh && chgrp ltc /var/lib/ltc/ltc.sh && chmod u+x /var/lib/ltc/ltc.sh


#Volume
VOLUME ["/var/lib/ltc"]

# node service
EXPOSE 9333

# RPC service
EXPOSE 9332


#cmd to exeucute 
#CMD ["bitcoind"]
ENTRYPOINT ["/var/lib/ltc/ltc.sh"]
