BootStrap: docker
From: nvidia/cuda:8.0-cudnn6-devel

%post

    apt-get -y update
    apt-get -y install vim wget perl python python-pip python-dev

    # install tensorflow
    pip install --upgrade pip
    pip install tensorflow-gpu

