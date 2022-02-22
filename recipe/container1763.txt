# FMRIPREP from poldracklab

BootStrap: docker
From: poldracklab/fmriprep:1.0.7

%runscript
    exec /usr/local/miniconda/bin/fmriprep "$@"



    

%post
################################################################################
# Create directories to enable access to common HPCC mount points
################################################################################
chmod -R a+rX /usr/local/miniconda
chmod +x /usr/local/miniconda/bin/*
mkdir -p /mnt/home
mkdir -p /mnt/research
mkdir -p /mnt/research/schmaelzlelab
mkdir -p /mnt/dfs17
mkdir -p /mnt/ffs17
mkdir -p /mnt/local
mkdir -p /mnt/ls15
mkdir -p /opt/software
mkdir -p /mnt/home/schmaelz
mkdir -p /mnt/veiled
 
