Bootstrap: docker
From: alpine:3.6

%runscript
    exec /usr/bin/nmap "$@"

%labels
   AUTHOR remy.dernat@umontpellier.fr

%post
    echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories
    apk update && \
    apk add --no-cache nmap nbtscan iperf nethogs netcat-openbsd
