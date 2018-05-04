FROM ubuntu:16.04
MAINTAINER Roberto Di Remigio  <roberto.d.remigio@uit.no>
RUN apt-get --yes -qq update && \
    apt-get --yes -qq upgrade && \
    apt-get --yes -qq install bzip2 \
                              cpio \
                              curl \
                              g++ \
                              gcc \
                              gfortran \
                              git \
                              libboost-all-dev \
                              libopenmpi-dev \
                              openmpi-bin \
                              python-dev \
                              python-pip \
                              zlib1g-dev \
                              wget && \
    rm -rf /var/lib/apt/lists/*
SHELL ["/bin/bash", "-c"]
ENV MKL_URL "http://registrationcenter-download.intel.com/akdlm/irc_nas/tec/12147/l_mkl_2017.4.239.tgz"
# Copy stuff from host to container
COPY silent-mkl.cfg Deps/mkl/
RUN cd $WORKDIR/Deps && \
    curl -Ls $MKL_URL | tar -xz -C mkl --strip-components=1 && \
    cd mkl && \
    ./install.sh --silent=silent-mkl.cfg && \
    cd $WORKDIR/Deps && \
    rm -rf l_mkl_2017.4.239.tgz mkl && \
    groupadd mightybuilder && \
    adduser --disabled-password --gecos '' --system --shell /bin/bash mightybuilder && \
    adduser mightybuilder sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    adduser mightybuilder mightybuilder
USER mightybuilder
ENV HOME /home/mightybuilder
WORKDIR $HOME
RUN mkdir -p $HOME/Deps && \
    cd $HOME/Deps && \
    export cmake_url="https://cmake.org/files/v3.10/cmake-3.10.2-Linux-x86_64.tar.gz" && \
    export target_path=$HOME/Deps/cmake && \
    mkdir -p $target_path && \
    curl -Ls $cmake_url | tar -xz -C $target_path --strip-components=1 && \
    rm -rf cmake-3.10.2-Linux-x86_64.tar.gz && \
    pip install --user virtualenv pipenv --upgrade pip && \
    source /opt/intel/bin/compilervars.sh intel64
ENV PATH $HOME/Deps/cmake/bin:$HOME/.local/bin:$PATH
ENV LD_LIBRARY_PATH $HOME/.local/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
ENV MATH_ROOT=$MKLROOT
