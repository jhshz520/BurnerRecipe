Bootstrap:docker  
From:ubuntu:latest  

%files
/mnt/home/dolsonem/containerized_avida_test $SINGULARITY_ROOTFS/containerized_avida_test

%post  
echo "This section happens once after bootstrap to build the image."  
apt-get update
apt-get --assume-yes install criu

mkdir -p /mnt/home
mkdir -p /mnt/research
mkdir -p /mnt/dfs17
mkdir -p /mnt/ffs17
mkdir -p /mnt/local
mkdir -p /mnt/ls15
mkdir -p /opt/software
mkdir -p /code  

%runscript
echo "This gets run when you run the image!" 
SHELL="$(getent passwd $USER | awk -F: '{print $NF}')"
SHELL=${SHELL:-/bin/bash}
if [[ "$@" == "" ]]; then
  exec env -i TERM="$TERM" HOME="$HOME" $SHELL -l
else
  exec env -i TERM="$TERM" HOME="$HOME" $@
fi

cd $SINGULARITY_ROOTFS/containerized_avida_test/results/run_1
cp -r $SINGULARITY_ROOTFS/containerized_avida_test/configs .
./avida
