BootStrap: docker
From: centos:centos7

%post
yum -y update && yum -y upgrade
yum -y install epel-release && yum -y update && yum -y upgrade
# you need to create the top level directories since there is no overlay on CentOS-6
# specific to my setup
mkdir -p /local-storage /mnt/beegfs /baycells/home /baycells/scratch /c6/shared /c6/eb /local/gensoft2 /c6/shared/rpm /Bis/Scratch2 /mnt/beegfs /pasteur

yum -y install https://github.com/jgraph/drawio-desktop/releases/download/v8.0.6/draw.io-x86_64-8.0.6.rpm

yum -y install \
libXtst libXScrnSaver GConf2 alsa-lib  \
libcanberra-gtk2 libcanberra adwaita-gtk2-theme PackageKit-gtk3-module \
which xorg-x11-fonts-Type1 liberation-sans-fonts

%runscript
draw.io  "$@"
