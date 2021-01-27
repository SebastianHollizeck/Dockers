FROM centos:8

MAINTAINER Sebastian Hollizeck

#install system update and install packages
RUN yum update -y && yum install -y git cmake gcc-c++ make zlib-devel

WORKDIR /opt

#clone and compile
RUN git clone https://github.com/shahcompbio/hmmcopy_utils.git hmmcopy && cd /opt/hmmcopy && cmake . && make

#add the bin folder to the path
ENV PATH=/opt/hmmcopy/bin/:$PATH

CMD ["readCounter"]
