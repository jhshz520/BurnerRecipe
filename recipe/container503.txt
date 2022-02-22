Bootstrap: debootstrap
MirrorURL: http://archive.ubuntu.com/ubuntu/
OSVersion: xenial
Include: software-properties-common
%post
    add-apt-repository -s ppa:kernsuite/kern-1
    apt-add-repository multiverse
    apt-get update
    apt-get dist-upgrade -y
    apt-get install -y cassbeam python-qwt5-qt4 python-qwt5-doc tempo purify casacore-dev casacore-doc casacore-tools casarest casacore-data meqtrees-timba python-purr python-tigger python-meqtrees-cattery python-owlcat python-kittens python-pyxis python-meqtrees-timba rpfits lofar meqtrees libmeqtrees-timba0 aoflagger wsclean sagecal mt-imager oskar python-casacore obit parseltongue greatcmakecookoff sopt libcasasynthesis-dev libcasasynthesis1 libcasa-casa2 libcasa-coordinates2 libcasa-derivedmscal2 libcasa-fits2 libcasa-images2 libcasa-lattices2 libcasa-meas2 libcasa-measures2 libcasa-mirlib2 libcasa-ms2 libcasa-msfits2 libcasa-python2 libcasa-python3-2 libcasa-scimath-f2 libcasa-scimath2 libcasa-tables2 python3-casacore psrcat presto tempo2 psrchive multinest dspsr python-presto python-sourcery chgcentre python-tkp python-katversion python-katpoint python-katdal python-rfimasker python-pip python-virtualenv
    apt-get clean
    pip install --upgrade pip virtualenv
