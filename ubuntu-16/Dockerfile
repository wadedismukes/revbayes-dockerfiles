FROM ubuntu:16.04

RUN apt-get update \
    && apt-get install -y --no-install-recomemends \
                    software-properties-common \
    && apt-add-repository multiverse


RUN useradd docker \
    && mkdir /home/docker \
    && chown docker:docker /home/docker

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        bash-completion \
        tar \
        curl \
        unzip \
        git

RUN export CC=gcc-4.9
RUN export CXX=g++-4.9
RUN update-alternatives --install /usr/bin/gcc  gcc /usr/bin/gcc-4.9  90
RUN update-alternatives --install /usr/bin/g++  g++ /usr/bin/g++-4.9  90
RUN curl -O -L https://dl.bintray.com/boostorg/release/1.71.0/source/boost_1_71_0.tar.gz
RUN tar -xzf boost_1_71_0.tar.gz
RUN cd boost_1_71_0 \
    && ./bootstrap.sh --with-libraries=atomic,chrono,filesystem,system,regex,thread,date_time,program_options,math,serialization \
    && ./b2 link=static 

ENV BOOST_ROOT=/boost_1_71_0
ENV BOOST_INCLUDE_DIR=/boost_1_71_0
ENV BOOST_LIBRARY_DIR=/boost_1_71_0/stage/lib

# feel free to change this 
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && /usr/sbin/update-locale LANG=en_US.UTF-8

RUN git clone --depth 1 https://github.com/revbayes/revbayes.git revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh
RUN export PATH=$PATH:/revbayes/projects/cmake

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
CMD rb