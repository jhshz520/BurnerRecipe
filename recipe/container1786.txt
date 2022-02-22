Bootstrap: docker
From: tensorflow/tensorflow:1.5.0-gpu-py3

%help

To install python libraries after this image is built, create a virtual environment that uses the system packages with `virtualenv --system-site-packages venv && source venv/bin/activate`, then use `pip` as usual.


%environment
  # use bash as default shell
  SHELL=/bin/bash
  export SHELL

%setup
  # runs on host - the path to the image is $SINGULARITY_ROOTFS

%post
  # post-setup script

  # load environment variables
  . /environment

  # use bash as default shell
  echo 'SHELL=/bin/bash' >> /environment
  chmod +x /environment

  # default mount paths
  mkdir -p /scratch /data /usr/bin

  apt-get update
  apt-get install -y cmake libcupti-dev libyaml-dev wget unzip locales
  apt-get clean
  locale-gen en_US.UTF-8

  pip3 install --upgrade pip
  pip3 install numpy tqdm virtualenv

  wget https://github.com/mgbellemare/Arcade-Learning-Environment/archive/v0.6.0.zip
  unzip v0.6.0.zip
  cd Arcade-Learning-Environment-0.6.0
  rm -rf build
  mkdir build
  cd build
  cmake -DUSE_SDL=OFF -DUSE_RLGLUE=OFF -DBUILD_EXAMPLES=OFF ..
  make -j 4

  cd ../
  pip3 install .

%runscript
  # executes with the singularity run command
  # delete this section to use existing docker ENTRYPOINT command

%test
  # test that script is a success
