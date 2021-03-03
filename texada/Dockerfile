FROM ubuntu:14.04

# install dependencies:
RUN apt-get update
RUN apt-get install -y libboost-all-dev libgtest-dev cmake g++ wget unzip git

# compile and setup google test:
RUN cd /usr/src/gtest && cmake CMakeLists.txt && make && cp *.a /usr/lib

# download and install spot:
RUN cd ~/ && wget https://www.lrde.epita.fr/dload/spot/spot-1.2.5.tar.gz && tar -zxvf spot-1.2.5.tar.gz
RUN cd ~/spot-1.2.5/ && ./configure && make && make check && make install

# download texada:
RUN cd ~/ && git clone https://github.com/ModelInference/texada.git

# setup environment to run texada:
ENV TEXADA_HOME=/root/texada
ENV LD_LIBRARY_PATH=/usr/local/lib

# set up the uservars.mk file based on the example that's there:
RUN cd ~/texada && cp uservars.mk.example uservars.mk

# only change the SPOT_INCL location since all other location
# vars are available system-wide and need not be changed:
RUN cd ~/texada && sed -i "/^SPOT_INCL:=/c\SPOT_INCL:=${PWD%/*}/spot-1.2.5/src" uservars.mk

# build texada and texadatest
RUN cd ~/texada && make

# run texadatest to make sure all the tests pass
RUN ~/texada/texadatest
