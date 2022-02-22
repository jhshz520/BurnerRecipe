BootStrap: docker
From: ubuntu:16.04

%post
	apt-get -y update
	apt-get -y install libgsl-dev
%runscript
	./run.sh # optional
