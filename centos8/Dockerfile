FROM centos:centos8

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
RUN yum update -y
RUN yum group install -y "Development Tools"
RUN yum install -y cmake boost-devel
RUN yum install -y bash-completion 
RUN yum install -y curl
RUN yum install -y unzip
RUN yum install -y less
RUN yum install -y git

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