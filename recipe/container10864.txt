Bootstrap: docker
From: ubuntu:16.04

IncludeCmd: yes

%labels
    MAINTAINER icaoberg@cmu.edu
    WEBSITE http://www.cbd.cmu.edu/icaoberg
    VERSION 1.0

%runscript
    exec /bin/bash "$@"

%post
    apt-get update
    echo "Install Gimp"
    apt-get install -y gimp

    if [ ! -d /images ]; then mkdir /images; fi
    if [ ! -d /projects ]; then mkdir /projects; fi
    if [ ! -d /containers ]; then mkdir /containers; fi
    if [ ! -d /share ]; then mkdir /share; fi
    if [ ! -d /scratch ]; then mkdir /scratch; fi

####################################################################################
%appenv gimp
    APP=/usr/bin/gimp
    export APP

%apphelp gimp
    For more information about goto visit https://www.gimp.org/

%apprun gimp
    gimp "$@"
