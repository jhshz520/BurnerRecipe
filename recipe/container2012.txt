Bootstrap: docker
From: tensorflow/tensorflow:1.5.0-gpu-py3

%post
    apt-get update && apt-get -y install locales
    locale-gen en_US.UTF-8
    apt-get install -y git wget python3-dev python3-pip
    apt-get clean

    apt-get install -y libcupti-dev
    apt-get install -y openslide-tools

    pip3 install --upgrade pip
    pip3 install keras
    pip3 install openslide-python
