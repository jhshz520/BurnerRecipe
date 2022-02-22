Bootstrap: docker
From: tensorflow/tensorflow

%post
    apt-get -y install git-core
    git clone https://github.com/GPflow/GPflow.git
    cd GPflow
    pip install .