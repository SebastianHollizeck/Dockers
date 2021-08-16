from ubuntu:20.04

MAINTAINER Sebastian Hollizeck sebastian.hollizeck@petermac.org

ENV OCTOPUS_VERSION 0.7.2
ENV HTSLIB_VERSION 1.12
ENV BOOST_VERSION 1.75.0
ENV BOOST_VERSION_UNDER 1_75_0


# install all the requirements that are easy
RUN  apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends software-properties-common && add-apt-repository ppa:ubuntu-toolchain-r/test && apt-get install -y --no-install-recommends git wget gcc-10 libgmp3-dev git-all python3 autoconf build-essential g++ python-dev autotools-dev libicu-dev libbz2-dev libboost-all-dev liblzma-dev

#set the workingdir
WORKDIR /opt/

#install the newest cmake maybe (hopefully the version we have is high enough)

#RUN apt remove --purge --auto-remove cmake

RUN apt-get install -y libcurl4-openssl-dev

# install htslib
RUN wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VERSION}/htslib-${HTSLIB_VERSION}.tar.bz2 \
    && tar -xjf htslib-${HTSLIB_VERSION}.tar.bz2 \
    && rm -f htslib-${HTSLIB_VERSION}.tar.bz2 \
    && cd /opt/htslib-${HTSLIB_VERSION}/ \
    && make \
    && make install

# install BOOST
RUN wget -O boost_${BOOST_VERSION}.tar.gz https://sourceforge.net/projects/boost/files/boost/${BOOST_VERSION}/boost_${BOOST_VERSION_UNDER}.tar.gz/download \
    && tar xzvf boost_${BOOST_VERSION}.tar.gz \
    && rm -f boost_${BOOST_VERSION}.tar.gz \
    && cd boost_${BOOST_VERSION_UNDER}/ \
    && ./bootstrap.sh \
    && ./b2 \
    && ./b2 install

# finally install octopus
RUN wget -O octopus_${OCTOPUS_VERSION}.tar.gz https://github.com/luntergroup/octopus/archive/refs/tags/v0.7.2.tar.gz \
    && tar xzvf octopus_${OCTOPUS_VERSION}.tar.gz \
    && rm -f octopus_${OCTOPUS_VERSION}.tar.gz

RUN apt-get install -y cmake
RUN cd /opt/octopus-${OCTOPUS_VERSION}/build \
    && cmake .. \
    && make install \
    && cp /opt/octopus-${OCTOPUS_VERSION}/bin/octopus /usr/local/bin/


#remove the libraries again to reduce the size of the image
RUN rm -r htslib-${HTSLIB_VERSION} && rm -r boost_${BOOST_VERSION_UNDER} && rm -r octopus-${OCTOPUS_VERSION}

ENTRYPOINT ["octopus"]
CMD ["-h"]
