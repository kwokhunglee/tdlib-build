FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install make git zlib1g-dev libssl-dev gperf php cmake clang-6.0 libc++-dev libc++abi-dev -y
RUN git clone https://github.com/tdlib/td.git
RUN cd td && git checkout v1.6.0 && rm -rf build && mkdir build && cd build
RUN export CXXFLAGS="-stdlib=libc++" 
RUN cd /td/build && CC=/usr/bin/clang-6.0 CXX=/usr/bin/clang++-6.0 cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/usr/local -DTD_ENABLE_LTO=ON -DCMAKE_AR=/usr/bin/llvm-ar-6.0 -DCMAKE_NM=/usr/bin/llvm-nm-6.0 -DCMAKE_OBJDUMP=/usr/bin/llvm-objdump-6.0 -DCMAKE_RANLIB=/usr/bin/llvm-ranlib-6.0 /td
RUN cd /td/build && cmake --build . --target prepare_cross_compiling
RUN cd /td && php SplitSource.php
RUN cd /td/build  && cmake --build . --target install
RUN cd /td && php SplitSource.php --undo
RUN apt-get install wget -y
RUN wget -O go.tgz https://studygolang.com/dl/golang/go1.14.4.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go.tgz && rm go.tgz