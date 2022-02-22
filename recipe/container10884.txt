Bootstrap: docker
From: ubuntu:16.04

IncludeCmd: yes

%labels
  MAINTAINER icaoberg
  EMAIL icaoberg@alumni.cmu.edu
  WEBSITE http://linus.cbd.cs.cmu.edu
  VERSION v1.0

%runscript
      exec /usr/bin/python "$@"

%post
    /usr/bin/apt-get update && /usr/bin/apt-get -y upgrade
    /usr/bin/apt-get -y install module-init-tools
    /usr/bin/apt-get update --fix-missing
    /usr/bin/apt-get install -y --no-install-recommends apt-utils
    /usr/bin/apt-get install -y build-essential
    /usr/bin/apt-get install -y rar unrar p7zip-full
    
    if [ ! -d /images ]; then mkdir /images; fi
    if [ ! -d /projects ]; then mkdir /projects; fi
    if [ ! -d /containers ]; then mkdir /containers; fi
    if [ ! -d /share ]; then mkdir /share; fi
    if [ ! -d /scratch ]; then mkdir /scratch; fi
    if [ ! -d /webservers/pfenningweb ]; then mkdir -p /webservers/pfenningweb; fi
    
####################################################################################
%appenv unrar
   BEST_APP=unrar
   export BEST_APP

%apprun unrar
   unrar "$@"
   
####################################################################################
%appenv rar
   BEST_APP=rar
   export BEST_APP
   
%apprun rar
   rar "$@"

####################################################################################
%appenv 7z 
   BEST_APP=7z
   export BEST_APP

%apprun 7z
   7z "$@"
