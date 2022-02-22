BootStrap: docker
From: ubuntu:latest

%post
    apt-get update
    apt-get -y install python3-pip locales
    pip3 install asciinema
    locale-gen en_GB.UTF-8


%environment
    LANG=en_GB.UTF-8
    LANGUAGE=en_GB:en
    LC_ALL=en_GB.UTF-8
    export LANG LANGUAGE LC_ALL

%runscript
exec asciinema "$@"
