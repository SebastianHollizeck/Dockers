FROM alpine

MAINTAINER Sebastian Hollizeck

RUN mkdir /opt/freebayes

WORKDIR /opt/freebayes

RUN wget https://github.com/ekg/freebayes/releases/download/v1.3.1/freebayes-v1.3.1 && chmod +x freebayes-v1.3.1 && ln -s /opt/freebayes/freebayes-v1.3.1 /usr/bin/freebayes 

ENTRYPOINT ["freebayes"]
CMD ["-h"]
