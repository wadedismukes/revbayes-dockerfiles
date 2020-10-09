FROM ubuntu:latest as base

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
RUN git clone --depth 1 https://github.com/revbayes/revbayes.git revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh

FROM src as prod
COPY --from=build /revbayes/projects/cmake/rb /revbayes/
COPY --from=build /revbayes/projects/cmake/build/core/librb-core.a /revbayes/
COPY --from=build /revbayes/projects/cmake/build/revlanguage/librb-parser.a /revbayes/
COPY --from=build /revbayes/projects/cmake/build/libs/liblibs.a /revbayes/

ENTRYPOINT ["/revbayes/rb"]