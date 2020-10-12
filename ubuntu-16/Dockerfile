FROM ubuntu:16.04 as base

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
                    software-properties-common \
    && apt-add-repository multiverse


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
    && ./b2 link=static \
    && cd ..

ENV BOOST_ROOT=/boost_1_71_0
ENV BOOST_INCLUDE_DIR=/boost_1_71_0
ENV BOOST_LIBRARY_DIR=/boost_1_71_0/stage/lib

FROM base as src
COPY /home/runner/work/revbayes-dockerfiles/revbayes-dockerfiles/revbayes ./revbayes
ENV PATH=$PATH:./revbayes

RUN cd ./revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh \
        && mv rb ./revbayes/rb
FROM src as prod
CMD ["./revbayes/rb"]