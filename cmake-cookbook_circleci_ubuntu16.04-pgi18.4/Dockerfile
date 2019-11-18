FROM ubuntu:16.04

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
                      libboost-all-dev \
                      libpython3-all-dev \
                      libzmq3-dev \
                      pkg-config \
                      python3-dev \
                      python3-pip \
                      rpm \
                      uuid-dev \
 && rm -rf /var/lib/apt/lists/*

# Run common commands
COPY run_commands /opt/docker/bin/run_commands
RUN /opt/docker/bin/run_commands

ENV PGI_VERSION 18.4
ENV PGI_HOME /opt/pgi/linux86-64/$PGI_VERSION
ENV PGI_BIN_DIR $PGI_HOME/bin
ENV PGI_LIB_DIR $PGI_HOME/lib
ENV PGI_MAN_DIR $PGI_HOME/man
ENV PGI_OMPI_DIR $PGI_HOME/mpi/openmpi
ENV LM_LICENSE_FILE $LM_LICENSE_FILE:$PGI_HOME/license.dat

ENV PATH $PGI_BIN_DIR:$PGI_OMPI_DIR/bin:$PATH:/root/.local/bin:/opt/cmake/bin:/opt/ninja:/opt/conda/bin
ENV LD_LIBRARY_PATH /root/.local/lib:$PGI_LIB_DIR${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
ENV MANPATH $PGI_MAN_DIR:$PGI_OMPI_DIR/man:$MANPATH

SHELL ["/bin/bash"]
