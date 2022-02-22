Bootstrap: docker
From: ubuntu:18.04

%labels
Maintainer Matthew Flister

%help
This container runs includes available PacBio apps as of 09/18/2019.

%environment
    SHELL=/bin/bash
    export PATH="/opt/miniconda2/bin:$PATH"

%post
    # default mount points
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts

    # Install necessary packages
    apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        gcc-multilib \
        libboost-all-dev \
        libhdf5-serial-dev \
        zlib1g-dev \
        python3-pip \
        pkg-config \
        python-dev \
        python-setuptools \
        wget \
        bzip2
    apt-get clean

    # install miniconda
    wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh -O miniconda2.sh
    bash miniconda2.sh -b -p /opt/miniconda2
    rm miniconda2.sh
    export PATH="/opt/miniconda2/bin:$PATH"

    # install pacbio apps
    conda install -c bioconda \
        bam2fastx \
        bax2bam \
        blasr \
        pbgcpp \
        genomicconsensus \
        isoseq3 \
        lima \
        minorseq \
        pbbam \
        pbccs \
        pbcommand \
        pbcopper \
        pbcore \
        pbcoretools \
        pblaa \
        pbalign \
        pbmm2 \
        pbsv \
        recalladapters \
        pb-falcon \
        pb-dazzler \
        pb-assembly 

    wget https://github.com/lh3/minimap2/releases/download/v2.17/minimap2-2.17_x64-linux.tar.bz2 && tar -xvf minimap2-2.17_x64-linux.tar.bz2
    mv minimap2-2.17_x64-linux/minimap2 /opt/miniconda2/bin
    rm -rf minimap2-2.17_x64-linux*
