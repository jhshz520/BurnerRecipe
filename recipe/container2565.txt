Bootstrap: docker
From: ubuntu:latest

%post
	apt-get update
	apt-get install -y wget
	apt-get install -y bzip2
	apt-get install -y vim
	wget https://repo.continuum.io/archive/Anaconda3-5.1.0-Linux-x86_64.sh
	bash Anaconda3-5.1.0-Linux-x86_64.sh -f -b -p $HOME/anaconda
	export PATH="$HOME/anaconda/bin:$PATH"
	conda update -y conda
	pip install --upgrade tensorflow
	pip install keras
	conda update -y conda
