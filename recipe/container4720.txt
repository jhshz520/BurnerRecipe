BootStrap: docker
From: ubuntu:16.04

%help
    This container runs a Jupyter Notebook on a compute node.

%labels
    Maintainer Matthew Flister

%post
    # make mount points
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts
    # install deps
    apt-get update && apt-get install -y --no-install-recommends \
        python3 \
        python3-dev \
        python3-pip \
        python3-setuptools \
        python \
        python-dev \
        python-pip \
        python-setuptools \
        build-essential \
        gcc-multilib
    apt-get clean
    #install python pkgs
    pip install --no-cache-dir --upgrade pip==9.0.3
    pip3 install --no-cache-dir --upgrade pip==9.0.3
    pip install jupyter ipykernel scipy numpy pandas matplotlib biopython jupyterlab
    pip3 install jupyter ipykernel scipy numpy pandas matplotlib biopython jupyterlab

