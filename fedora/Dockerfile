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

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh 

FROM src as prod
COPY --from=build /revbayes/projects/cmake/rb /revbayes/
COPY --from=build /revbayes/projects/cmake/build/core/librb-core.a /revbayes/
COPY --from=build /revbayes/projects/cmake/build/revlanguage/librb-parser.a /revbayes/
COPY --from=build /revbayes/projects/cmake/build/libs/liblibs.a /revbayes/

ENTRYPOINT ["/revbayes/rb"]