# Singularity recipe for HPLinpack

Bootstrap: docker
From: centos:7

%post
# update system
yum install -y epel-release
yum install -y \
    tar gzip curl net-tools numactl libmlx4 librdmacm libibverbs dapl rdma \
yum clean all
# get intel c++ and benchmark redistributables
mkdir /install
pushd /install
curl -fSsL https://software.intel.com/sites/default/files/managed/4b/33/l_comp_lib_2017.2.174_comp.cpp_redist.tgz | tar zxvpf  -
curl -fSsL http://registrationcenter-download.intel.com/akdlm/irc_nas/9752/l_mklb_p_2017.3.018.tgz | tar zxvpf -
# install intel c++ and benchmark redistributables into /intel
cd l_comp_lib_2017.2.174_comp.cpp_redist
./install.sh -i /intel -e
cd ..
cp -r l_mklb_p_2017.3.018/benchmarks_2017/linux/mkl /intel
popd
rm -rf /install
