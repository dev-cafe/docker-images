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
                              libatlas-dev \
                              libboost-all-dev \
                              libhwloc-dev \
                              liblapack-dev \
                              libnuma-dev \
                              python-dev \
                              python-pip \
                              wget && \
    rm -rf /var/lib/apt/lists/*
SHELL ["/bin/bash", "-c"]
RUN groupadd mightybuilder && \
    adduser --disabled-password --gecos '' --system --shell /bin/bash mightybuilder && \
    adduser mightybuilder sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    adduser mightybuilder mightybuilder
USER mightybuilder
ENV HOME /home/mightybuilder
WORKDIR $HOME
ENV PGI_URL "https://www.dropbox.com/s/aktmjxbfet46xqs/pgilinux-2017-174-x86_64.tar.gz"
RUN mkdir -p $HOME/Deps/pgilinux && \
    cd $HOME/Deps && \
    curl -Ls $PGI_URL | tar -xz -C pgilinux && \
    cd pgilinux && \
    export PGI_SILENT=true && \
    export PGI_ACCEPT_EULA=accept && \
    export PGI_INSTALL_DIR=$HOME/Deps/pgi && \
    export PGI_INSTALL_TYPE=single && \
    export PGI_INSTALL_NVIDIA=false && \
    export PGI_INSTALL_MANAGED=true && \
    export PGI_INSTALL_JAVA=false && \
    export PGI_INSTALL_AMD=false && \
    export PGI_INSTALL_MPI=true && \
    export PGI_MPI_GPU_SUPPORT=false && \
    ./install && \
    cd $HOME/Deps && \
    rm -rf pgilinux-2017-174-x86_64.tar.gz pgilinux && \
    export cmake_url="https://cmake.org/files/v3.5/cmake-3.5.2-Linux-x86_64.tar.gz" && \
    export target_path=$HOME/Deps/cmake/3.5.2 && \
    rm -rf cmake-3.5.2-Linux-x86_64.tar.gz && \
    mkdir -p $target_path && \
    curl -Ls $cmake_url | tar -xz -C $target_path --strip-components=1 && \
    export cmake_url="https://cmake.org/files/v3.10/cmake-3.10.2-Linux-x86_64.tar.gz" && \
    export target_path=$HOME/Deps/cmake/3.10.2 && \
    mkdir -p $target_path && \
    curl -Ls $cmake_url | tar -xz -C $target_path --strip-components=1 && \
    rm -rf cmake-3.10.2-Linux-x86_64.tar.gz && \
    pip install --user virtualenv pipenv --upgrade pip
ENV PGI_VERSION 17.4
ENV PGI_HOME    $HOME/Deps/pgi/linux86-64/$PGI_VERSION
ENV PGI_BIN_DIR $PGI_HOME/bin
ENV PGI_LIB_DIR $PGI_HOME/lib
ENV PGI_MAN_DIR $PGI_HOME/man
ENV LM_LICENSE_FILE $LM_LICENSE_FILE:$PGI/license.dat
ENV PATH $PGI_HOME/bin:$PGI_HOME/mpi/openmpi/bin:$HOME/.local/bin:$PATH
ENV LD_LIBRARY_PATH $PGI_LIB_DIR:$HOME/.local/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
ENV MANPATH $PGI_MAN_DIR:$MANPATH
