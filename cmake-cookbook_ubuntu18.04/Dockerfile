FROM ubuntu:18.04

# Set an encoding to make things work smoothly.
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# Add a timestamp for the build. Also, bust the cache.
ADD http://worldclockapi.com/api/json/utc/now /opt/docker/etc/timestamp

# Install system packages
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get --yes -qq update \
 && apt-get --yes -qq upgrade \
 && apt-get --yes -qq install \
                      bzip2 \
                      cpio \
                      curl \
                      doxygen \
                      emacs-nox \
                      g++ \
                      g++-mingw-w64 \
                      gcc \
                      gcc-mingw-w64 \
                      gfortran \
                      gfortran-mingw-w64 \
                      git \
                      gosu \
                      graphviz \
                      libacl1-dev \
                      libblas-dev \
                      libboost-filesystem-dev \
                      libboost-python-dev \
                      libboost-test-dev \
                      libeigen3-dev \
                      liblapack-dev \
                      libncurses5-dev \
                      libopenmpi-dev \
                      libpython3-all-dev \
                      libx11-dev \
                      libxt-dev \
                      libzmq3-dev \
                      openmpi-bin \
                      patchelf \
                      pkg-config \
                      python3-dev \
                      python3-pip \
                      rpm \
                      sudo \
                      uuid-dev \
                      valgrind \
                      vim-nox \
 && apt-get --yes -qq clean \
 && rm -rf /var/lib/apt/lists/*

# Run common commands
COPY run_commands /opt/docker/bin/run_commands
RUN /opt/docker/bin/run_commands

# Add a file for users to source
COPY entrypoint_source /opt/docker/bin/entrypoint_source

# Add a file that wraps that for use with the `ENTRYPOINT`.
COPY entrypoint /opt/docker/bin/entrypoint

# Ensure that all containers start with tini and the user selected process.
ENTRYPOINT [ "/opt/docker/bin/tini", "--", "/opt/docker/bin/entrypoint" ]

# Provide a default command (`bash`), which will start if the user doesn't specify one.
CMD [ "/bin/bash" ]
