# Deploys the keycloak server
BootStrap: docker
From: ubuntu:latest

%environment

    DEBIAN_FRONTEND=noninteractive

%setup

    cp keycloak/keycloakAlt.sh ${SINGULARITY_ROOTFS}
    cp keycloak/keyPwdSing.sh ${SINGULARITY_ROOTFS}

%post

    # Download and install wget, unzip, and java
    apt-get update -y
    apt-get install -y --no-install-recommends apt-utils
    apt-get install -y wget unzip default-jre default-jdk iproute curl libxml2-utils 

    # Go to the srv directory
    cd /srv

    # Download and unzip Keycloak
    wget https://downloads.jboss.org/keycloak/3.4.0.Final/keycloak-3.4.0.Final.zip
    unzip keycloak-3.4.0.Final.zip
    rm keycloak-3.4.0.Final.zip

    mv /keycloakAlt.sh /srv/keycloakAlt.sh
    mv /keyPwdSing.sh /srv/keyPwdSing.sh

    # make the anchor
    # this file determines how much extra "free" space
    # will be made available on the container
    # the file is deleted at runtime to free the space
    # this free space is necessary for keycloak's database
    dd if=/dev/zero of=/srv/out.dat bs=1M count=512

    chmod a+rwx -R /srv
    umask 0


%runscript

    # Start keycloak when the container is run
    # the keycloakStart.sh script determines the local IP on which
    # the keycloak server should listen
    #exec /srv/keycloakStart.sh False CanDIG admin admin user user
    exec /srv/keycloakAlt.sh
