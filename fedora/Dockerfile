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
RUN git clone --depth 1 https://github.com/revbayes/revbayes.git revbayes

ENV PATH=$PATH:/revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh \
        && mv rb /revbayes/rb
FROM src as prod
ENTRYPOINT ["/revbayes/rb"]