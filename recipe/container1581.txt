Bootstrap: docker
From: ubuntu:latest

%files
mpi-ping.c /mpi-ping.c

%labels
AUTHOR souchal@apc.in2p3.fr
version 1.0

%environment
LD_LIBRARY_PATH=/usr/local/lib/
export LD_LIBRARY_PATH

%post

apt-get update && apt-get -y install software-properties-common wget build-essential sgml-base rsync xml-core openssh-client
add-apt-repository universe
apt-get update && apt-get -y install cmake git gfortran openmpi-common openmpi-bin libopenmpi-dev
apt-get clean

%runscript
mpicc /mpi-ping.c 
