#!/bin/bash
# 
# Tru Huynh <tru@pasteur.fr>
# 2017/06/07: initial version

BootStrap: docker
From: alpine:latest

%runscript
echo "This is what happens when you run the container..."
/bin/sh

%post
echo "Hello from inside the container"
apk update && apk upgrade
touch /`date -u -Iseconds`

# tars.pasteur.fr specific (no overlays on CentOS-6)
mkdir -p /pasteur/{homes,scratch,entites} /local/{scratch,flash} /mount/gensoft2 

%labels
MAINTAINER truatpasteurdotfr
