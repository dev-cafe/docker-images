FROM devcafe/ubuntu16.04-pgi17.4:latest
MAINTAINER Roberto Di Remigio  <roberto.d.remigio@uit.no>
SHELL ["/bin/bash", "-c"]
RUN mkdir -p $HOME/Downloads && \
    cd $HOME/Deps && \
    mkdir -p ninja && \
    curl -Ls https://goo.gl/4g5Jjv | tar -xz -C ninja --strip-components=1 && \
    echo "-- Done with Ninja" && \
    cd $HOME/Downloads && \
    curl -LOs http://bitbucket.org/eigen/eigen/get/3.3.4.tar.gz && \
    tar xzf 3.3.4.tar.gz &>/dev/null && \
    cd eigen-eigen-5a0156e40feb && \
    $HOME/Deps/cmake/3.10.2/bin/cmake -H. -Bbuild_eigen -DCMAKE_INSTALL_PREFIX=$HOME/Deps/eigen &>/dev/null && \
    $HOME/Deps/cmake/3.10.2/bin/cmake --build build_eigen -- install &>/dev/null && \
    cd $HOME/Downloads && \
    rm -rf eigen-eigen-5a0156e40feb 3.3.4.tar.gz && \
    echo "-- Done with Eigen 3.3.4" && \
    curl -LOs https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.1/src/hdf5-1.10.1.tar.bz2 && \
    tar xjf hdf5-1.10.1.tar.bz2 &> /dev/null && \
    cd hdf5-1.10.1 && \
    CC=pgcc FC=pgf90 ./configure --prefix=$HOME/Deps/hdf5 --enable-build-mode=debug \
              --enable-shared --enable-fortran &> /dev/null && \
    make install &> /dev/null && \
    rm -rf hdf5-1.10.1 hdf5-1.10.1.tar.bz2 && \
    cd $HOME/Downloads && \
    echo "-- Done with HDF5 1.10.1" && \
    curl -Ls https://repo.continuum.io/archive/Anaconda2-5.1.0-Linux-x86_64.sh > conda.sh && \
    bash conda.sh -b -p $HOME/Deps/conda &> /dev/null && \
    rm -rf conda.sh && \
    PATH=$HOME/Deps/conda/bin${PATH:+:$PATH} && \
    conda config --set always_yes yes --set changeps1 no &> /dev/null && \
    conda update -q conda &> /dev/null && \
    echo "-- Done with Anaconda 5.1.0"
ENV PATH $HOME/Deps/ninja:$HOME/Deps/conda/bin:$PATH
ENV LD_LIBRARY_PATH $HOME/Deps/hdf5/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
