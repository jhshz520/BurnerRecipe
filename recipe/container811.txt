BootStrap: docker
From: nvidia/cuda:8.0-cudnn6-runtime-ubuntu16.04

################################################################################
%labels
################################################################################
MAINTAINER Wolfgang Resch
VERSION v3

################################################################################
%environment
################################################################################
export PATH=/usr/local/sbin:/usr/sbin:/sbin:/bin:/usr/bin:/usr/local/bin:/usr/local/cuda/bin:
export PYTHONPATH=/usr/share/pdb2pqr:

################################################################################
%post
################################################################################

###
### install keras + tensorflow + other useful packages
###
apt-get update
apt-get install -y wget libhdf5-dev graphviz locales python3-dev python3-pip git python-pandas
locale-gen en_US.UTF-8
apt-get clean

pip3 install --upgrade pip
pip3 install tensorflow-gpu==1.4.0
pip3 install keras==2.0.8
pip3 install setuptools wheel Pillow scikit-learn matplotlib ipython==5.5.0
pip3 install h5py
pip3 install --upgrade notebook
pip3 install cython
pip3 install Biopython
pip3 install six

###
### destination for NIH HPC bind mounts
###
mkdir /gpfs /spin1 /gs2 /gs3 /gs4 /gs5 /gs6 /gs7 /gs8 /data /scratch /fdb /lscratch /pdb

