FROM debian:latest as base


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
RUN git clone --depth=1 https://github.com/revbayes/revbayes.git /revbayes
ENV PATH=$PATH:/revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh \
        && mv rb /revbayes/rb

FROM src as prod

ENTRYPOINT ["/revbayes/rb"]