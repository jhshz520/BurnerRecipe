Bootstrap: docker
From: gmichiels/python-client-base:latest

%files
    detect_sample.py /

%runscript
    python /detect_sample.py
