Bootstrap: docker
From: centos:6.9

%environment
    LD_LIBRARY_PATH=/mnt/abc/u/staff/hwleong/craylibs:$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH
    PATH=/mnt/abc/u/staff/hwleong/test/singularity/openmpi-2.1.0/bin:$PATH
    export PATH
    
%help
My test image for centos 6.9. Author: hwleong

%labels
Author: Hon Wai, Leong

%post
    echo "Installing Development tools"
    yum -y groupinstall "Development Tools"
    echo "Installing other utilities"
    yum -y install wget tcl
    echo "/mnt/abc/u/staff/hwleong/craylibs" >> /etc/ld.so.conf
    echo "export LD_LIBRARY_PATH=/mnt/abc/u/staff/hwleong/craylibs:$LD_LIBRARY_PATH" >>$SINGULARITY_ENVIRONMENT
    echo "export PATH=/mnt/abc/u/staff/hwleong/test/singularity/openmpi-2.1.0/bin:$PATH" >>$SINGULARITY_ENVIRONMENT
    echo "export OPAL_PREFIX=/mnt/abc/u/staff/hwleong/test/singularity/openmpi-2.1.0" >>$SINGULARITY_ENVIRONMENT
    touch /etc/sysconfig/xt
    mkdir -p /etc/opt/cray
    
%appenv mpi
    SCIF_APPBIN_mpi=/mnt/abc/u/staff/hwleong/singularity/openmpi-2.1.0/bin
    SCIF_APPLIB_mpi=/mnt/abc/u/staff/hwleong/singularity/openmpi-2.1.0/lib:/mnt/abc/u/staff/hwleong/craylibs
    export SCIF_APPBIN_mpi SCIF_APPLIB_mpi
