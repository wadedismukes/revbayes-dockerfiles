FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y --no-install-recomemends \
                    software-properties-common \
    && apt-add-repository multiverse


RUN useradd docker \
    && mkdir /home/docker \
    && chown docker:docker /home/docker

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        libboost-all-devel \            
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