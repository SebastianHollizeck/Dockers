FROM shollizeck/hmmcopy:1.0.0

MAINTAINER Sebastian Hollizeck sebastian.hollizeck@petermac.org

# update the system and install R (need to install (enable) epel and powertool repo
# before R installation)
RUN yum update -y && yum install -y epel-release dnf-plugins-core \
    && yum config-manager --set-enabled powertools \
    && yum install -y libcurl-devel libxml2-devel


#link the bin into the path
ENV R_VERSION 4.0.3

#install this specific version so we dont get the whole shebang
RUN yum install -y https://cdn.rstudio.com/r/centos-8/pkgs/R-${R_VERSION}-1-1.x86_64.rpm && ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R && ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript

WORKDIR /opt/

# install ichorCNA
# get git repo and install r (could also use the release here)
RUN git clone https://github.com/broadinstitute/ichorCNA.git

RUN R --slave -e 'install.packages(c("BiocManager", "plyr", "RCurl", "optparse"), repos="https://mirror.aarnet.edu.au/pub/CRAN/")' &&  R --slave -e 'BiocManager::install(c("HMMcopy","GenomeInfoDb", "GenomicRanges"), update=TRUE, ask=FALSE)'

# install it (probably not necessary, but also not a big deal)
RUN R CMD INSTALL ichorCNA

#this way we have easy access to the scripts
WORKDIR /opt/ichorCNA/scripts

#and this way people will get the help right away
CMD ["Rscript", "runIchorCNA.R", "-h"]
