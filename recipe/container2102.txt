Bootstrap: docker
From: centos:latest

%help
This is a test container using the latest version of centos.  
Its purpose is just to perform basic tests of the singularity installation.

%labels
	Maintainter Kurt.J.Strosahl

%post
	echo "test image"

	echo "Installing Devlopment Tools YUM group"
	yum -y groupinstall "Development Tools"

	echo "installing kernel"
	yum -y install kernel kernel-devel
	
	echo "installing bind utils for testing."
	yum -y install bind-utils
	
	mkdir {/volatile,/cache}
%environment
BLACK='\e[0;30m'
BLUE='\e[0;34m' 
BBLUE='\e[1;34m'
GREEN='\e[0;32m'
BGREEN='\e[1;32m'
CYAN='\e[0;36m'  
BCYAN='\e[1;36m' 
RED='\e[0;31m'   
BRED='\e[1;31m'  
PURPLE='\e[0;35m'
BPURPLE='\e[1;35m'
BROWN='\e[0;33m' 
NORMAL='\e[m'

PS1="$BCYAN S $BBLUE\u$PURPLE@$BBLUE\h$BGREEN ~>$NORMAL ";export PS1

alias ll="ls -lsrt"
