BootStrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%runscript
    python3 /opt/main.py

%post
    echo "Hello from inside the container"
    sed -i 's/$/ universe/' /etc/apt/sources.list
    touch /usr/bin/nvidia-smi
    apt-get -y update
    apt-get -y --force-yes install blender fortune libxv1 libx11-6 lolcat python3 python3-pip python3-tk wget
    pip3 install --upgrade pip
    pip3 install gym jupyter lmdb matplotlib numpy pandas scipy six tqdm
    pip3 install http://download.pytorch.org/whl/cu80/torch-0.3.1-cp35-cp35m-linux_x86_64.whl 
    pip3 install torch torchvision    
    /usr/games/lolcat /etc/lsb-release
    /usr/games/fortune | /usr/games/lolcat
    wget -O /opt/main.py https://raw.githubusercontent.com/pytorch/examples/master/mnist/main.py
