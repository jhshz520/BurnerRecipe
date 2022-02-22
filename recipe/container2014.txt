Bootstrap: docker
From: nvidia/cuda:9.1-cudnn7-devel-ubuntu16.04

%setup
%post
    # Make sure cuda is in the right place
    ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/libcuda.so.1 
    # apt install -y python3-numpy python3-dev python3-pip python3-wheel
    apt update && apt upgrade -y
    apt install -y git libcupti-dev locales openjdk-8-jdk curl openssl libssl-dev
    echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list
    curl https://bazel.build/bazel-release.pub.gpg | apt-key add -
    apt update && apt install -y bazel

    # Locales were messed up for some reason, manually setting otherwise pip will complain
    dpkg-reconfigure locales
    locale-gen en_US.UTF-8
    export LC_ALL=en_US.UTF-8

    # Install python 3.6
    curl https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz | tar xJf -
    cd Python-3.6.4
    ./configure
    make -j6
    make install
    # Clean up python source code
    cd / && rm -rf Python-3.6.4

    yes | pip3 install six numpy wheel numpy

    # TF dependency TODO: Try linking python to python3
    apt install -y python2.7-minimal

    ln -s /usr/bin/python2.7 /usr/bin/python

