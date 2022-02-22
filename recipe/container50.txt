BootStrap: docker
From: kaixhin/cuda-theano:7.5

%setup
    # commands to be executed on host outside container during bootstrap

%post
    # create bind points for NIH HPC environment
    mkdir /gpfs /spin1 /gs2 /gs3 /gs4 /gs5 /gs6 /data /scratch /fdb /lscratch

    # download and run NIH HPC NVIDIA driver installer
    wget ftp://helix.nih.gov/CUDA/cuda4singularity
    chmod 755 cuda4singularity
    ./cuda4singularity --verbose
    rm cuda4singularity

    # set some vars in the environment
    echo "
PATH=/usr/local/cuda-7.5/bin:\$PATH
LD_LIBRARY_PATH=/usr/local/cuda/lib64:\$LD_LIBRARY_PATH
LD_LIBRARY_PATH=/usr/local/cuda/extras/CUPTI/lib64:\$LD_LIBRARY_PATH
CUDA_HOME=/usr/local/cuda
export PATH LD_LIBRARY_PATH CUDA_HOME" >>/environment
 
%runscript
    # commands to be executed when the container runs
 
%test
    # commands to be executed within container at close of bootstrap process

