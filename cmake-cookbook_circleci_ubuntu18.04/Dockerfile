FROM ubuntu:18.04

# Set an encoding to make things work smoothly.
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# Add a timestamp for the build. Also, bust the cache.
ADD http://worldclockapi.com/api/json/utc/now /opt/docker/etc/timestamp

RUN apt-get --yes -qq update \
 && apt-get --yes -qq upgrade \
 && apt-get --yes -qq install \
                      bzip2 \
                      cpio \
                      curl \
                      doxygen \
                      g++ \
                      g++-mingw-w64 \
                      gcc \
                      gcc-mingw-w64 \
                      gfortran \
                      gfortran-mingw-w64 \
                      git \
                      graphviz \
                      libacl1-dev \
                      libboost-all-dev \
                      libncurses5-dev \
                      libopenmpi-dev \
                      libpython3-all-dev \
                      libx11-dev \
                      libxt-dev \
                      libzmq3-dev \
                      openmpi-bin \
                      pkg-config \
                      python3-dev \
                      python3-pip \
                      rpm \
                      uuid-dev \
 && rm -rf /var/lib/apt/lists/*

# Run common commands
COPY run_commands /opt/docker/bin/run_commands
RUN /opt/docker/bin/run_commands

ENV PATH $PATH:/root/.local/bin:/opt/cmake/bin:/opt/ninja:/opt/conda/bin

ENV LD_LIBRARY_PATH /root/.local/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}

SHELL ["/bin/bash"]
