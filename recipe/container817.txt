Bootstrap: docker
From: tensorflow/tensorflow:latest-gpu

%post
mkdir -p \
  /mnt/home \
  /mnt/research \
  /mnt/veiled \
  /mnt/local \
  /mnt/dfs17 \
  /mnt/ffs17 \
  /mnt/ls15 \
  /opt/software

%runscript
exec $(which python) $@

