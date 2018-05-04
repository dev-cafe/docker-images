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
ENV INTEL_URL "https://www.dropbox.com/s/75nmbp19l25fm6x/parallel_studio_xe_2018_update2_professional_edition.tgz"
# Copy stuff from host to container
COPY silent-parallel-studio.cfg Deps/parallel_studio_xe_2018_update2_professional_edition/
RUN cd $WORKDIR/Deps && \
    curl -Ls $INTEL_URL | tar -xz -C parallel_studio_xe_2018_update2_professional_edition --strip-components=1 && \
    cd parallel_studio_xe_2018_update2_professional_edition && \
    ./install.sh --silent=silent-parallel-studio.cfg && \
    cd $WORKDIR/Deps && \
    rm -rf parallel_studio_xe_2018_update2_professional_edition && \
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
    source /opt/intel/bin/compilervars.sh -arch intel64 -platform linux
ENV PATH $HOME/Deps/cmake/bin:$HOME/.local/bin:$PATH
ENV LD_LIBRARY_PATH $HOME/.local/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
ENV MATH_ROOT=$MKLROOT
