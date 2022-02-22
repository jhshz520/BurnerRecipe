Bootstrap: yum
OSVersion: 7
MirrorURL: http://ftp2.scientificlinux.org/linux/scientific/7x/x86_64/os
Include: yum

%runscript
    exec echo "module load openmpi/3.0.0"
%labels
   AUTHOR ivy2@uchicago.edu
%post
   yum -y update
   yum -y install wget emacs vi make automake autoconf gcc gcc-c++ which python perl gcc-gfortran
   wget https://www.open-mpi.org/software/ompi/v3.0/downloads/openmpi-3.0.0.tar.gz
   tar xvf openmpi-3.0.0.tar.gz
   cd openmpi-3.0.0
   ./configure --enable-mpi-cxx --enable-mpi-fortran --enable-mpi-cxx-seek
   make
   make install

   

