Bootstrap: docker
From: ubuntu:latest

%runscript

	echo "Hopefully this works!"

%post

	echo "Installing git"
	apt-get update
	apt-get install -y git

	echo "Installing python"
	apt-get install -y software-properties-common python-software-properties
	add-apt-repository ppa:fkrull/deadsnakes
	apt-get update
	apt-get install -y python2.7

	echo "Installing pip and virtualenv"
	apt-get install -y python-pip python-dev build-essential
	pip install --upgrade pip
	pip install --upgrade virtualenv
	
	echo "Installing python-tk"
	apt-get install -y python-tk

	echo "Installing TensorFlow"
	pip install tensorflow

	echo "Installing Keras"
	pip install keras

	echo "Installing matplotlib, sklearn, h5py"
	pip install matplotlib
	pip install sklearn
	pip install h5py
