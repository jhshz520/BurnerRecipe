Bootstrap: docker
From: debian:latest

IncludeCmd: yes

%labels
    MAINTAINER icaoberg@alumni.cmu.edu
    WEBSITE http://linus.cbd.cs.cmu.edu
    VERSION 1.0

%runscript
    exec /bin/bash "$@"

%post
    echo "Update and upgrade"
    /usr/bin/apt-get update && apt-get install -y --no-install-recommends apt-utils
    /usr/bin/apt-get install -y octave

####################################################################################
%appenv octave
    APP=/usr/bin/octave
    export APP

%apphelp octave
    For more information about goto visit http://www.octave.info

%apprun octave
    octave "$@"
