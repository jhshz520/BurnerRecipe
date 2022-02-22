BootStrap: docker
From: ubuntu:artful

%post
    apt-get -y update && apt-get -y install python3 python3-pip texlive-xetex && pip3 install jupyter && pip3 install --upgrade pip
