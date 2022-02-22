Bootstrap: docker
From: centos:6.9

%help
My test image for centos 6.9. Author: hwleong

%labels
Author: Hon Wai, Leong

%post
    echo "Installing Development tools"
    yum -y groupinstall "Development Tools"
    echo "Installing other utilities"
    yum -y install wget tcl
