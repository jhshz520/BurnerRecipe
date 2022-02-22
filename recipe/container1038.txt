Bootstrap:docker  
From:ubuntu:latest  

%labels
MAINTAINER Eduard Wisernig and Joe Melton, ECCC

%environment
BASE_DIR=/code
export BASE_DIR

%runscript
echo "Congratulations! You got the container running!"
cd /code/testSingularity
bin/testSingularity

%post
mkdir -p /code
cd /code
apt update
apt install vim make libnetcdff-dev git gfortran netcdf-bin nano -y -f -m
git clone https://github.com/eduardwisernig/testSingularity.git
cd testSingularity
mkdir bin
make
cd ..
chmod -R 777 testSingularity