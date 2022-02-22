Bootstrap:docker  
From:alpine:latest

%labels
MAINTAINER Andy M

%environment
HELLO_BASE=/code
export HELLO_BASE

%runscript
echo "This script is executed when you 'singularity run' the image!" 
exec /bin/sh /code/hello.sh "$@"  

%post  
echo "This section is performed after you bootstrap to build the image."  
apk update
mkdir -p /code  
apk add vim nano bash 
echo "echo Hello World" >> /code/hello.sh
chmod u+x /code/hello.sh  
