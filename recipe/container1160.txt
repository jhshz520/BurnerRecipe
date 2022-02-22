
# Singularity container definition 
# Cuda 8.0 run time on CentOS 6
# 

# ref https://hub.docker.com/r/nvidia/cuda/
# ref https://gitlab.com/nvidia/cuda/blob/centos6/9.0/runtime/Dockerfile
# ref http://singularity-hub.org/containers/712


BootStrap: docker
From: nvidia/cuda:8.0-runtime-centos6
#From: nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04


%help
This container is a CentOS 6 with nvidia cuda runtime 

%runscript
	echo "zsh from inside the container..."
	/bin/zsh


%post
	#echo "Hello from inside the container"
	touch /THIS_IS_INSIDE_SINGULARITY
	yum -ty install vim bash zsh wget curl tar coreutils which util-linux-ng man \
			environment-modules telnet nc \
			ipmitool \
			pciutils \
			epel-release  # sl6 may need diff mech to enable epel
			#libpng libpng-devel libpng-static \
			#openmotif openmotif-devl openmotif22 \
			# telnet client for troubleshooting license manager connection

	yum -ty install dkms \
			cuda-nvidia-kmod-common nvidia-kmod \
			pcp-pmda-nvidia-gpu \
			xorg-x11-drv-nvidia xorg-x11-drv-nvidia-gl xorg-x11-drv-nvidia-devel \
		 	xorg-x11-drv-nvidia-libs 
			# xorg-x11-drv-nvidia-diagnostic  
			# nvidia-settings nvidia-uvm-kmod nvidia-xconfig nvidia-modprobe # obsolete
			#xorg-x11-drv-nvidia-libs-387.26-1
			# org-x11-drv-nvidia-libs should provide /usr/lib64/libcuda.so.1
			# from cuda repo ::
			# name=cuda
			# baseurl=http://developer.download.nvidia.com/compute/cuda/repos/rhel6/x86_64
			# enabled=1
			# gpgcheck=1
			# gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA

	echo "end"                  >> /THIS_IS_INSIDE_SINGULARITY
	date                        >> /THIS_IS_INSIDE_SINGULARITY

%labels
MAINTAINER  Tin Ho tin'at'lbl.gov


## sudo    /opt/singularity-2.4.2/bin/singularity build -w ./perf_tools.simg ./Singularity
## sudo    /opt/singularity-2.4.2/bin/singularity build -w ./sl6_lbl.simg ./sl6_lbl.def

