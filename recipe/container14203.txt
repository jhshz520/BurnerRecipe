Bootstrap: docker
From: ubuntu@sha256:fff16eea1a8ae92867721d90c59a75652ea66d29c05294e6e2f898704bdb8cf1

%runscript
    exec echo "This is an Ubuntu 20.04 LTS Container with Miniconda v4.8.3!!"

%files
   
%environment
   CONDA_INSTALL_PATH="/usr/local/miniconda3"
   CONDA_BIN_PATH="/usr/local/miniconda3/bin"
   export PATH="$CONDA_BIN_PATH:$PATH"
   export LC_ALL=C.UTF-8
   export LANG=C.UTF-8

%labels
   OWNER andreiprodan

%post
   echo "The post section is where you can install, and configure your container."  
   apt-get update && apt-get -y install wget     # Installing commonly used apps
   wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.8.3-Linux-x86_64.sh    # download and install Anaconda (miniconda, conda v.4.8.3)
   chmod +x Miniconda3-py38_4.8.3-Linux-x86_64.sh
   CONDA_INSTALL_PATH="/usr/local/miniconda3"
   ./Miniconda3-py38_4.8.3-Linux-x86_64.sh -b -p $CONDA_INSTALL_PATH
   rm Miniconda3-py38_4.8.3-Linux-x86_64.sh
   export PATH="/usr/local/miniconda3/bin:$PATH"      # cant create environments without this
