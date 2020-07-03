FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade
RUN apt-get install make git zlib1g-dev libssl-dev gperf php cmake g++
RUN git clone https://github.com/tdlib/td.git
RUN cd td && git checkout v1.6.0 && rm -rf build && mkdir build && cd build
RUN export CXXFLAGS="" && cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/usr/local -DTD_ENABLE_LTO=ON .. && cmake --build . --target prepare_cross_compiling
RUN cd .. && php SplitSource.php
RUN cd build && cmake --build . --target install
RUN cd .. && php SplitSource.php --undo
RUN cd ~ 
RUN wget -O go.tgz https://studygolang.com/dl/golang/go1.14.4.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go.tgz && rm go.tgz