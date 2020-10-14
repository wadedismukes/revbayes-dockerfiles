FROM centos:8 as base

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
RUN yum update -y
RUN yum group install -y "Development Tools"
RUN yum install -y cmake boost-devel
RUN yum install -y bash-completion 
RUN yum install -y curl
RUN yum install -y unzip
RUN yum install -y less
RUN yum install -y git

FROM base as src
RUN ls
COPY revbayes/revbayes ./revbayes
ENV PATH=$PATH:./revbayes

RUN cd ./revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh \
        && mv rb ./revbayes/rb
FROM src as prod
ENTRYPOINT ["./revbayes/rb"]