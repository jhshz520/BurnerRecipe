BootStrap: docker
From: debian:stretch
# more details at https://github.com/nongiach/arm_now

%runscript
echo "running arm_now  from the container:"
arm_now "$@"

%post
echo "Hello from inside the container"
sed -i -e 's,http://deb.debian.org,http://cdn-fastly.deb.debian.org,g' /etc/apt/sources.list
apt-get update && apt-get -y upgrade
apt-get -y install python3-pip python3-dev python3  git qemu  e2tools
git clone https://github.com/nongiach/arm_now
cd /arm_now && pip3 install -r requirements.txt && pip3 install .
# e2tools qemu

touch /singularity-`date +%Y%m%d-%H%M%S`

# specific to my setup, required if you don't have overlay support (CentOS-6)
# CentOS-7 host can ignore that mkdir line
mkdir -p /local-storage /mnt/beegfs /baycells/home /baycells/scratch /c6/shared /c6/eb /local/gensoft2 /c6/shared/rpm /Bis/Scratch2 /mnt/beegfs

