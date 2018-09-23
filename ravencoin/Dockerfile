FROM ubuntu:latest

ENV EDITOR vim
ENV SHELL bash

# setup to add bitcoin repository
RUN apt-get -q update && apt-get install software-properties-common --no-install-recommends -y -q && add-apt-repository ppa:bitcoin/bitcoin

RUN apt-get -q update && apt-get upgrade -y && apt-get install --no-install-recommends -y -q \
	build-essential \
	libtool \
	autotools-dev \
	automake \
	pkg-config \
	libssl-dev \
	libevent-dev \
	bsdmainutils \
	python3 \
	libboost-system-dev \
	libboost-filesystem-dev \
	libboost-chrono-dev \
	libboost-program-options-dev \
	libboost-test-dev \
	libboost-thread-dev \
	libqt5gui5 \
	libqt5core5a \
	libqt5dbus5 \
	qttools5-dev \
	qttools5-dev-tools \
	libprotobuf-dev \
	protobuf-compiler \
	miniupnpc \
	vim \
	libdb4.8-dev \
	libdb4.8++-dev \
	libdb4.8 \
	git \
	libzmq3-dev \
	libevent-2.1-6 \
	curl \
	htop 

# Pull the ravencoin distribution
RUN mkdir -p /Ravencoin && git clone https://github.com/RavenProject/Ravencoin.git /Ravencoin && cd /Ravencoin && git checkout -b v2.0.4.1 tags/v2.0.4.1 

# Build the software
RUN cd /Ravencoin && ./autogen.sh && ./configure && make && make install && rm -rf /Ravencoin

# Adding the user to the image 
#RUN useradd -s /bin/bash -m /var/lib/rvn rvn
RUN mkdir -p /var/lib/rvn && useradd -s /bin/bash -d /var/lib/rvn rvn
RUN chown rvn:rvn -R /var/lib/rvn


#Copy the script over to the image
COPY rvn.sh /var/lib/rvn/
RUN chown rvn /var/lib/rvn/rvn.sh && chgrp rvn /var/lib/rvn/rvn.sh && chmod u+x /var/lib/rvn/rvn.sh


#Volume
VOLUME ["/var/lib/rvn"]

# node service
EXPOSE 8767

#RPC port
EXPOSE 8766


#cmd to exeucute 
#CMD ["bitcoind"]
ENTRYPOINT ["/var/lib/rvn/rvn.sh"]
