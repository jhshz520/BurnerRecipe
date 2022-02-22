BootStrap: docker
From: centos:centos7

%post
yum -y update && yum -y upgrade
yum -y install git \
 libtool autoconf automake make \
 rpm-build wget 
# anything listed in the "BuildRequires:" of the spec file is listed below
# >= 2.4.3
# yum -y install libarchive-devel python

%runscript
# https://github.com/singularityware/singularity/releases/download/2.4.2/singularity-2.4.2.tar.gz
# https://github.com/singularityware/singularity/archive/2.4.2.tar.gz
D=`mktemp -d`
echo '***' && \
echo "building in $D" && \
echo '***' 
cd $D && \
wget https://github.com/singularityware/singularity/releases/download/2.4.2/singularity-2.4.2.tar.gz && \
(rpmbuild -ta singularity-2.4.2.tar.gz ) |tee  build.log && \
tar czvf built.tgz build.log ~/rpmbuild/{RPMS,SRPMS} && \
echo '***' && \
echo results in $D
echo '***'

