FROM fedora:latest

RUN dnf update \
    && dnf groupinstall "Development Tools" \
        cmake \
        boost-devel \         
        bash-completion \
        tar \
        curl \
        unzip \
        git

RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && /usr/sbin/update-locale LANG=en_US.UTF-8

RUN git clone --depth 1 https://github.com/revbayes/revbayes.git revbayes

RUN cd /revbayes/projects/cmake \
        && rm -rf build/ \
        && ./build.sh 

RUN export PATH=$PATH:/revbayes/projects/cmake
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
CMD rb