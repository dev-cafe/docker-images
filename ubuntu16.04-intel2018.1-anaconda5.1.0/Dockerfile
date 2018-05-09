FROM devcafe/ubuntu16.04-intel2018.1:latest
MAINTAINER Roberto Di Remigio  <roberto.d.remigio@uit.no>
SHELL ["/bin/bash", "-c"]
RUN mkdir -p $HOME/Downloads && \
    cd $HOME/Deps && \
    mkdir -p ninja && \
    export Ninja_URL="https://github.com/Kitware/ninja/releases/download/v1.8.2.g3bbbe.kitware.dyndep-1.jobserver-1/ninja-1.8.2.g3bbbe.kitware.dyndep-1.jobserver-1_x86_64-linux-gnu.tar.gz"
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
    curl -Ls https://repo.continuum.io/archive/Anaconda2-5.1.0-Linux-x86_64.sh > conda.sh && \
    bash conda.sh -b -p $HOME/Deps/conda &> /dev/null && \
    rm -rf conda.sh && \
    PATH=$HOME/Deps/conda/bin${PATH:+:$PATH} && \
    conda config --set always_yes yes --set changeps1 no &> /dev/null && \
    conda update -q conda &> /dev/null && \
    echo "-- Done with Anaconda 5.1.0"
ENV PATH $HOME/Deps/ninja:$HOME/Deps/conda/bin:$PATH
