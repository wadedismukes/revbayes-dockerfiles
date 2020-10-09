FROM fedora:latest as base

RUN dnf update \
    && dnf groupinstall -y "Development Tools"
RUN dnf groupinstall -y cmake \
        boost-devel \         
        bash-completion \
        tar \
        curl \
        unzip \
        git

FROM base as src
RUN git clone --depth 1 --branch development https://github.com/revbayes/revbayes.git revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh 

RUN export PATH=$PATH:/revbayes/projects/cmake
FROM src as prod
CMD ["rb"]