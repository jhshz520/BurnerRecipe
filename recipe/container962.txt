Bootstrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/$basearch/ 
Include: yum

%runscript
    echo "This is what happens when you run the container..."


%post
    echo "Hello from inside the container"
    yum -y update
    yum -y install vim-minimal bzip2-devel sqlite-devel xz-devel tk-devel gdbm-devel readline-devel openssl-devel git vim wget gcc make bzip2 patch gcc-c++
    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/miniconda
    export PATH="/opt/miniconda/bin:$PATH"
    conda install -c bioconda fastqc
