BootStrap: docker
From: debian:9

%label
    Maintainer remi-andre.olsen@scilifelab.se

%post
    apt-get update
    apt-get install -y git build-essential cmake libboost1.62-all-dev zlib1g-dev

    git clone https://github.com/vezzi/FRC_align.git
    cd FRC_align
    mkdir build
    cd build
    cmake ..
    make

    cp lib/bamtools/src/api/libbamtools.so* /lib
    cp ../bin/FRC /bin

    apt-get clean
    rm -rf /var/lib/apt/lists/*

    #UPPMAX stuff NOTE: Only testing for now, should use singulary run -B /sw:/sw etc container.img
    mkdir /sw
    mkdir /proj
    mkdir /pica
    mkdir /lupus

%runscript
    exec FRC "$@"
