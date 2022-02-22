BootStrap: docker
From: ubuntu:16.10

%help
   A container to have Ubuntu 16.10 (Yakkety Yak) build environment.
   The environment should be enough to build AlmaBTE as per
   http://www.almabte.eu/index.php/user-manual/

%runscript
    echo "This is what happens when you run the container..."


%post
    echo "Hello from inside the container"
    apt-get -y update
    apt-get -y --force-yes install vim mc build-essential cmake libboost-all-dev libhdf5-dev wget

