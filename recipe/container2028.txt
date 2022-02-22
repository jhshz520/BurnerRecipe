BootStrap: docker
From: alpine:3.7
# more details at https://github.com/UnaPibaGeek/ctfr

%runscript
echo "running ctfr.py  from the container:"
python3 /ctfr/ctfr.py "$@"

%post
echo "Hello from inside the container"
apk update
apk upgrade
apk add py3-pip python3-dev python3  git
git clone https://github.com/UnaPibaGeek/ctfr.git
cd /ctfr && pip3 install -r requirements.txt

touch /singularity-`date +%Y%m%d-%H%M%S`

# specific to my setup, required if you don't have overlay support (CentOS-6)
# CentOS-7 host can ignore that mkdir line
mkdir -p /local-storage /mnt/beegfs /baycells/home /baycells/scratch /c6/shared /c6/eb /local/gensoft2 /c6/shared/rpm /Bis/Scratch2 /mnt/beegfs

