bootstrap: docker
from: ubuntu:16.04

%post
	
	apt-get update
	apt-get install -y 	build-essential \
						python-dev \
						python-pip \
						procps \
						ufw

	pip install --upgrade pip
	pip install --upgrade \
					psiturk


%environment
    export LC_ALL=C
    export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
    export PSITURK_GLOBAL_CONFIG_LOCATION=~/.psiturkconfig
