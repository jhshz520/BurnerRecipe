Bootstrap: docker
From: tensorflow/tensorflow:1.3.0-gpu-py3

%post
    apt-get update && apt-get -y install locales
    locale-gen en_US.UTF-8
    apt-get install -y git wget python3-dev python3-pip
    apt-get clean
    apt-get install -y build-essential automake autoconf libtool

    apt-get install -y libcupti-dev
    apt-get install -y cuda-drivers
    pip3 install --upgrade pip
    pip3 install keras
    
    pip3 --no-cache-dir install \
            h5py \
            ipykernel \
            jupyter \
            matplotlib \
            bokeh \
            cython \
            numpy \
            pandas \
            Pillow \
            scipy \
            sklearn \
            odl
    python3 -m ipykernel.kernelspec

    #############################
    # install astra-toolbox
    apt-get install -y libboost-all-dev
    wget https://github.com/astra-toolbox/astra-toolbox/archive/v1.8.3.tar.gz
    tar xzf v1.8.3.tar.gz
    rm v1.8.3.tar.gz
    cd astra-toolbox-1.8.3
    cd build/linux
    ./autogen.sh   # when building a git version
    ./configure --with-cuda=/usr/local/cuda \
            --with-python=/usr/bin/python3 \
            --with-install-type=module
    make
    make install

