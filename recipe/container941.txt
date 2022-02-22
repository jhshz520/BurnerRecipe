BootStrap: docker
From: centos:centos7

%post
yum -y update && yum -y upgrade
yum -y install bzip2 freetype mesa-libGLU libXi libXrender mesa-dri-drivers
    curl http://download.blender.org/release/Blender2.79/blender-2.79-linux-glibc219-x86_64.tar.bz2 | tar -C /opt -xjvf -
# add directories
mkdir -p /proj

%runscript
PATH=/opt/blender-2.79-linux-glibc219-x86_64/:${PATH}
export PATH
/opt/blender-2.79-linux-glibc219-x86_64/blender "$@"
