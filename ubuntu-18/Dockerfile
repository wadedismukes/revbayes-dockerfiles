FROM ubuntu:18.04 as base

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
        git \
        libboost-dev \
        libboost-program-options-dev \ 
        libboost-date-time-dev \
        libboost-filesystem-dev \
        libboost-regex-dev \
        libboost-serialization-dev \
        libboost-system-dev \
        libboost-thread-dev

FROM base as src
RUN git clone --depth 1 --branch development https://github.com/revbayes/revbayes.git revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh
RUN export PATH=$PATH:/revbayes/projects/cmake
FROM src as prod
CMD ["rb"]