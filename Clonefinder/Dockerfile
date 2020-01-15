FROM python:3

#install the required linux packages
RUN apt-get update && apt-get -y --no-install-recommends install libgtk2.0 libgconf-2-4 git

#install the required python packages
RUN pip install --no-cache SciPy NumPy Biopython ete3 scikit-learn six

#we need to have a EULA accepted for this, so we might need to think about the spreading
COPY ./megax-cc_10.1.6-1_amd64.deb ./
RUN dpkg -i megax-cc_10.1.6-1_amd64.deb

#get the CloneFinder repo
#this is to invalidate the cache, if the repo changed
ADD https://api.github.com/repos/sebastianhollizeck/CloneFinderAPI/git/refs/heads/master version.json
RUN cd /opt/ && git  clone https://github.com/sebastianhollizeck/CloneFinderAPI

RUN mv /opt/CloneFinderAPI/clonefinder /opt/ && chmod +x /opt/clonefinder/clonefinder.py && rm -r /opt/CloneFinderAPI

ENV PATH=/opt/clonefinder:$PATH

ENTRYPOINT ["clonefinder.py"]
