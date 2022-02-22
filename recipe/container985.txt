BootStrap: docker
From: centos:centos7

%post
yum -y update && yum -y upgrade

# you need to create the top level directories since there is no overlay on CentOS-6
# specific to my setup
mkdir -p /local-storage /mnt/beegfs /baycells/home /baycells/scratch /c6/shared /c6/eb /local/gensoft2 /c6/shared/rpm /Bis/Scratch2 /mnt/beegfs /pasteur

# https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US
# 
yum -y install tar bzip2 wget curl
# installing in /opt/firefox
curl 'https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US' | awk -F'"' '/href/ {print "wget -O - ",$2,"| tar -C /opt  -xjvf -"}'| sh

# pulling from the chrome dependancy chain
yum -y install \
GConf2 \
adwaita-cursor-theme \
adwaita-icon-theme \
alsa-lib \
at \
at-spi2-atk \
at-spi2-core \
atk \
avahi-libs \
bc \
cairo \
cairo-gobject \
colord-libs \
cronie \
cronie-anacron \
crontabs \
cups-client \
cups-libs \
dconf \
desktop-file-utils \
ed \
emacs-filesystem \
file \
fontconfig \
fontpackages-filesystem \
freetype \
gdk-pixbuf2 \
gettext \
gettext-libs \
glib-networking \
gnutls \
graphite2 \
groff-base \
gsettings-desktop-schemas \
gtk-update-icon-cache \
gtk3 \
harfbuzz \
hicolor-icon-theme \
hwdata \
jasper-libs \
jbigkit-libs \
json-glib \
lcms2 \
less \
libX11 \
libX11-common \
libXScrnSaver \
libXau \
libXcomposite \
libXcursor \
libXdamage \
libXext \
libXfixes \
libXft \
libXi \
libXinerama \
libXrandr \
libXrender \
libXt \
libXtst \
libXxf86vm \
libcroco \
libdrm \
libepoxy \
libgomp \
libgusb \
libjpeg-turbo \
libmodman \
libpciaccess \
libpipeline \
libpng \
libproxy \
libsoup \
libthai \
libtiff \
libunistring \
libusbx \
libxcb \
libxshmfence \
m4 \
mailx \
make \
man-db \
mariadb-libs \
mesa-libEGL \
mesa-libGL \
mesa-libgbm \
mesa-libglapi \
mozjs17 \
nettle \
pango \
patch \
pixman \
polkit \
polkit-pkla-compat \
postfix \
psmisc \
redhat-lsb-core \
redhat-lsb-submod-security \
rest \
spax \
stix-fonts \
systemd-sysv \
sysvinit-tools \
time \
trousers \
wget \
which \
xdg-utils                                             
yum -y install mesa-dri-drivers libcanberra-gtk2 libcanberra adwaita-gtk2-theme PackageKit-gtk3-module

%runscript

# you need to bind mount /run for dconf...
/opt/firefox/firefox "$@"
