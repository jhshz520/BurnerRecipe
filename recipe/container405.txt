BootStrap: docker
From: alpine:3.6
# more details at https://keychest.net/roca and https://github.com/crocs-muni/roca 

%runscript
echo "running roca-detect from the container:"
roca-detect "$@"

%post
echo "Hello from inside the container"
apk update
apk upgrade
apk add py2-pip python-dev python libressl-dev libffi-dev swig gcc musl-dev
pip install roca-detect

touch /singularity-`date +%Y%m%d-%H%M%S`

# specific to my setup, required if you don't have overlay support (CentOS-6)
# CentOS-7 host can ignore that mkdir line
mkdir -p /local-storage /mnt/beegfs /baycells/home /baycells/scratch /c6/shared /c6/eb /local/gensoft2 /c6/shared/rpm /Bis/Scratch2 /mnt/beegfs

