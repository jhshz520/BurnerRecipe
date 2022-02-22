# Adapted from https://github.com/qiime2/vm-playbooks/blob/master/docker/Dockerfile

BootStrap: docker
From: continuumio/miniconda3:4.3.27p0

%runscript
/opt/conda/bin/qiime "$@"

%post
export QIIME2_RELEASE=2017.12
export LC_ALL=C.UTF-8
export LANG=C.UTF-8
export MPLBACKEND=agg
export PATH=/opt/conda/bin:${PATH}

# Required by qt
apt update && apt install -y libgl1-mesa-swx11
# conda update -q -y conda
conda install --file https://data.qiime2.org/distro/core/qiime2-${QIIME2_RELEASE}-conda-linux-64.txt
qiime dev refresh-cache
