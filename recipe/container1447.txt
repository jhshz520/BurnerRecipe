BootStrap: docker
From: nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04


%environment

  export PATH=$PATH:/usr/local/cuda/bin/
  export CUDA_PATH=/usr/local/cuda
  #export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH
  #export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}

%post

    echo "sym link cuda"
    ln -s /usr/local/cuda/bin/nvcc /bin/nvcc

    echo "Apt-getting packages"
    apt-get update && apt-get -y install locales
    locale-gen en_US.UTF-8

    apt-get -y install  build-essential \
		    git \
        cmake \
        g++ \
        vim \
        wget \
        gdb \
        libpng-dev \
        freeglut3-dev

    apt-get clean

    echo "Manually installing glew packages"

    cd /

    wget http://mirrors.kernel.org/ubuntu/pool/main/g/glew/libglew1.10_1.10.0-3_amd64.deb
    dpkg -i libglew1.10_1.10.0-3_amd64.deb
    rm libglew1.10_1.10.0-3_amd64.deb

    wget http://mirrors.kernel.org/ubuntu/pool/main/g/glew/libglew-dev_1.10.0-3_amd64.deb
    dpkg -i libglew-dev_1.10.0-3_amd64.deb
    rm libglew-dev_1.10.0-3_amd64.deb


    apt-get clean



    if [ -d "/yaml-cpp"]; then

        echo "Found yaml-cpp"
    else

        echo "installing yaml-cpp"
        cd /
        git clone https://github.com/jbeder/yaml-cpp.git
        cd yaml-cpp && mkdir build && cd build
        cmake ..
        make
        make install
        make clean
    fi



%test
    echo "hello dad!"
