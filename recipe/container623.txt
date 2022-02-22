Bootstrap: docker
From: tensorflow/tensorflow:1.3.0-gpu-py3

%post
    apt-get update && apt-get -y install locales
    locale-gen en_US.UTF-8
    apt-get install -y git wget python3-dev python3-pip
    apt-get clean

    apt-get install -y libcupti-dev
    pip3 install --upgrade pip
    pip3 install keras
