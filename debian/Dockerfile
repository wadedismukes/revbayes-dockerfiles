FROM debian:testing as base

RUN apt-get update \
    && apt-add-repository multiverse


RUN apt-get update \
        build-essential \
        cmake \
        libboost-all-devel \
        bash-completion \
        tar \
        curl \
        unzip \
        git


FROM base as src
RUN git clone --depth 1 --branch development https://github.com/revbayes/revbayes.git revbayes
RUN cd /revbayes/projects/cmake \
        && ./build.sh 

RUN export PATH=$PATH:/revbayes/projects/cmake
FROM src as prod
CMD ["rb"]