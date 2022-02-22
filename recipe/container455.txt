bootstrap:docker
From:pvdb90/multiqc


%post
mkdir -p /boot
mkdir -p /cvmfs
mkdir -p /mnt/home
mkdir -p /mnt/research
mkdir -p /mnt/dfs17
mkdir -p /mnt/ffs17
mkdir -p /mnt/local
mkdir -p /mnt/ls15
mkdir -p /opt/software
chmod o+r /opt/conda/lib/python2.7/site-packages/.wh.conda-4.3.14-py2.7.egg-info

