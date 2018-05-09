FROM devcafe/ubuntu16.04-pgi17.4:latest
MAINTAINER Roberto Di Remigio  <roberto.d.remigio@uit.no>
SHELL ["/bin/bash", "-c"]
RUN mkdir -p $HOME/Downloads && \
    cd $HOME/Deps && \
    mkdir -p ninja && \
    export Ninja_URL="https://github.com/Kitware/ninja/releases/download/v1.8.2.g3bbbe.kitware.dyndep-1.jobserver-1/ninja-1.8.2.g3bbbe.kitware.dyndep-1.jobserver-1_x86_64-linux-gnu.tar.gz" && \
    curl -Ls $Ninja_URL | tar -xz -C ninja --strip-components=1 && \
    echo "-- Done with Ninja" && \
    cd $HOME/Downloads && \
    curl -LOs http://bitbucket.org/eigen/eigen/get/3.3.4.tar.gz && \
    tar xzf 3.3.4.tar.gz &>/dev/null && \
    cd eigen-eigen-5a0156e40feb && \
    $HOME/Deps/cmake/3.11.1/bin/cmake -H. -Bbuild_eigen -DCMAKE_INSTALL_PREFIX=$HOME/Deps/eigen &>/dev/null && \
    $HOME/Deps/cmake/3.11.1/bin/cmake --build build_eigen -- install &>/dev/null && \
    cd $HOME/Downloads && \
    rm -rf eigen-eigen-5a0156e40feb 3.3.4.tar.gz && \
    echo "-- Done with Eigen 3.3.4" && \
    curl -LOs https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.2/src/hdf5-1.10.2.tar.bz2 && \
    tar xjf hdf5-1.10.2.tar.bz2 &> /dev/null && \
    cd hdf5-1.10.2 && \
    CC=pgcc FC=pgf90 ./configure --prefix=$HOME/Deps/hdf5 --enable-build-mode=debug \
              --enable-shared --enable-fortran &> /dev/null && \
    make install &> /dev/null && \
    rm -rf hdf5-1.10.2 hdf5-1.10.2.tar.bz2 && \
    cd $HOME/Downloads && \
    echo "-- Done with HDF5 1.10.2"
ENV PATH $HOME/Deps/ninja:$PATH
ENV LD_LIBRARY_PATH $HOME/Deps/hdf5/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
