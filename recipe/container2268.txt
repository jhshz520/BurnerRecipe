####
# Defines a Singularity container with GPU and MPI enabled TensorFlow
# https://www.tensorflow.org/install/install_sources#tested_source_configurations
####

BootStrap: docker
From: nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

%environment
  export PATH=${PATH-}:/usr/lib/jvm/java-8-openjdk-amd64/bin/:/usr/local/cuda/bin
  export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
  export CUDA_HOME=/usr/local/cuda
  export LD_LIBRARY_PATH=${LD_LIBRARY_PATH-}:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64

%post
  apt update 
  apt-get install -y python-pip mpich wget
  pip install mpi4py
  pip install --no-cache-dir tensorflow-gpu

  # Patch container to work on Titan
  wget https://raw.githubusercontent.com/olcf/SingularityTools/master/Titan/TitanBootstrap.sh
  sh TitanBootstrap.sh
  rm TitanBootstrap.sh

