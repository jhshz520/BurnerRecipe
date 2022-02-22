Bootstrap: docker
From: ubuntu:16.04

# Maintained by:

# Jan-Bernard Marsman, PhD
# Cognitive Neuroscience Center
# Department of Neuroscience
# University Medical Center Groningen
#
# Contact: j.b.c.marsman [at] umcg.nl
#
# March 2018 :version 1.1

%environment
    SINGULARITY_SHELL="/bin/bash"
    PATH=$PATH:/usr/bin/cnc

%setup
    mkdir -p  $SINGULARITY_ROOTFS/root/.irods
    mkdir $SINGULARITY_ROOTFS/usr/bin/cnc

    # bind point for data directory
    mkdir $SINGULARITY_ROOTFS/data

%files
    scripts/* /usr/bin/cnc
    #irods_environment.json /root/.irods/
    
%post
    # make imported scripts executable
    chmod 755 /usr/bin/cnc/*
    
    
    apt-get update
    apt-get install -y wget 
    apt-get install -y apt-transport-https
    apt-get install -y progress
    apt-get install -y emacs
    
    apt-get install -y environment-modules lmod
    
    # add neurodebian repository
    wget -O- http://neuro.debian.net/lists/xenial.de-md.libre | tee /etc/apt/sources.list.d/neurodebian.sources.list
    apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net:80 0xA5D32F012649A5A9

    # add irods icommands 
    wget -qO - https://packages.irods.org/irods-signing-key.asc | apt-key add -
    echo "deb [arch=amd64] https://packages.irods.org/apt/ xenial main" | tee /etc/apt/sources.list.d/renci-irods.list

    apt-get update
        
    # add datalad
    apt-get install -y datalad

    # install dependencies (cmake)
    apt-get install -y cmake pkg-config

    # install dcm2niix
    apt-get install -y dcm2niix

    # install icommands
    apt-get install -y irods-icommands

    mkdir /software

%runscript
    exec cnc_convert "$@" 
