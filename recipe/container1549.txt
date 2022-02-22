Bootstrap: docker
From: centos:7

%labels
   AUTHOR sampedro@colorado.edu

%post
   useradd -u 515 -m slurm
   useradd -u 992 -m munge
   yum -y update
   yum -y install epel-release
   yum -y groupinstall 'Development Tools'
   yum -y install sssd wget strace iproute munge munge-devel pam-devel openssl openssl-devel readline-devel perl-devel
   cd ~ && wget https://download.schedmd.com/slurm/slurm-17.02.9.tar.bz2
   rpmbuild -ta slurm-17.02.9.tar.bz2
   cd ~/rpmbuild/RPMS/x86_64
   rpm -ivh slurm-pam_slurm-17.02.9-1.el7.centos.x86_64.rpm slurm-plugins-17.02.9-1.el7.centos.x86_64.rpm slurm-munge-17.02.9-1.el7.centos.x86_64.rpm slurm-perlapi-17.02.9-1.el7.centos.x86_64.rpm slurm-17.02.9-1.el7.centos.x86_64.rpm slurm-devel-17.02.9-1.el7.centos.x86_64.rpm
