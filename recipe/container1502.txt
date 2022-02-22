bootstrap: docker
from: ubuntu:16.04

%post
  apt-get update
  apt-get install -y wget

  mkdir /pycharm-src && cd /pycharm-src
  wget https://download.jetbrains.com/python/pycharm-community-2017.3.2.tar.gz
  tar -xvzf pycharm-community-2017.3.2.tar.gz
