BootStrap: docker
From: alpine:latest

%runscript
echo "running pdftk from the container:"
pdftk "$@"

%post
echo "Hello from inside the container"
apk update
apk upgrade
apk add pdftk
touch /singularity-`date +%Y%m%d-%H%M%S`

%labels
MAINTAINER truatpasteurdotfr

