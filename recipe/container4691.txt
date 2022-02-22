Bootstrap: docker
From: ubuntu:16.04

%labels
Maintainer Matthew Flister
Version 09.06.18

%help
This container runs AmpliconArchitect.

%environment
    SHELL=/bin/bash
    PATH=/opt/programs/mosek/8/tools/platform/linux64x86/bin:$PATH
    LD_LIBRARY_PATH=/opt/programs/mosek/8/tools/platform/linux64x86/bin:$LD_LIBRARY_PATH
    MOSEKLM_LICENSE_FILE=/home/$USER/.mosek/8/licenses
    AA_DATA_REPO=/rcc/stor1/refdata/ampliconarchitect/data_repo
    AA_SRC=/opt/programs/AmpliconArchitect-master/src
    export SHELL PATH LD_LIBRARY_PATH  MOSEKLM_LICENSE_FILE AA_DATA_REPO AA_SRC

%post
    # default mount points
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts

    # install packages
    apt-get update && apt-get install -y --no-install-recommends \
	build-essential \
	python-dev \
	gfortran \
	python-numpy \
	python-scipy \
	python-matplotlib \
	python-pip \
	python-setuptools \
	zlib1g-dev \
	samtools \
	wget \
	unzip
    apt-get clean


    # python packages
    pip install pysam Flask

    # install mosek
    mkdir -p /opt/programs
    mkdir -p /opt/output
    mkdir -p /opt/input
    cd /opt/programs && wget http://download.mosek.com/stable/8.0.0.60/mosektoolslinux64x86.tar.bz2
    cd /opt/programs && tar xf mosektoolslinux64x86.tar.bz2
    cd /opt/programs/mosek/8/tools/platform/linux64x86/python/2/ && python setup.py install

    # install ampliconarchitect
    cd /opt/programs && wget https://github.com/virajbdeshpande/AmpliconArchitect/archive/master.zip
    cd /opt/programs && unzip master.zip
