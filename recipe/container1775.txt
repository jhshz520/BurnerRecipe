BootStrap: docker
From: weatherlab/centos6.6_intel

%labels
MAINTAINER Xin Zhang
SPECIES EKDMOS

%runscript
    echo "Welcome, this is Singularity container for Intel"

%environments
    DISPLAY=:0.0
    export DISPLAY
    PATH=/usr/local/bin:${PATH}
    export PATH
    LD_LIBRARY_PATH=/opt/intel/composer_xe_2013.2.146/compiler/lib/intel64:/usr/local/lib:${LD_LIBRARY_PATH}
    export LD_LIBRARY_PATH

%post
    echo "Hello from inside the container"
    source /opt/intel/bin/compilervars.sh intel64
    yum update
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.rpm.sh | bash
    yum -y install wget tar git-lfs
    cd /usr/local/src
    wget --no-check-certificate https://www.open-mpi.org/software/ompi/v2.1/downloads/openmpi-2.1.0.tar.gz
    tar xf openmpi-2.1.0.tar.gz
    rm -f openmpi-2.1.0.tar.gz
    cd openmpi-2.1.0
    export FC=ifort
    export CC=icc
    export CXX=icpc
    opal_check_cma_happy=0 ./configure --enable-mpi-cxx
    make -j2 all && make install
    cd /usr/local/src
    rm -rf openmpi-2.1.0
    source /opt/intel/bin/compilervars.sh intel64

