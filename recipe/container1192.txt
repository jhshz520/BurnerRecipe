Bootstrap: docker
From: ubuntu:trusty

%setup
mkdir -p $SINGULARITY_ROOTFS/src
cp -Rv . $SINGULARITY_ROOTFS/src

%post 

## Install the validator
apt-get update && \
apt-get install -y curl && \
curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
apt-get remove -y curl && \
apt-get install -y nodejs && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

npm install -g /src

%runscript
exec /usr/bin/bids-validator $@
