BootStrap: docker
From: visus/visus:singularity

%runscript
  echo "Arguments: <optional_port> on which to run the server (default: 8080)"
  re='^[0-9]+$'
  PORT=${1:-8080}
  echo $PORT | grep "[^0-9]" > /dev/null 2>&1
  if [ "$?" -eq "0" ]; then
    # If the grep found something other than 0-9 then it's not an integer.
    echo "WARNING: Invalid port specified ($1)"
    echo "         Using default port 8080."
    PORT=8080
  fi
  umask 022
  mkdir /tmp/visus
  cp -r /visus/config /tmp/visus
  cp -r /visus/apache2 /tmp
  cd /tmp/apache2
	mv ports.conf ports.conf.orig
  sed "s/80/$PORT/" ports.conf.orig > ports.conf
	mv sites-enabled/webviewer.conf sites-enabled/webviewer.conf.orig
  sed "s/80/$PORT/" sites-enabled/webviewer.conf.orig > sites-enabled/webviewer.conf

  echo "Starting visus server"
  echo "Connect to `hostname`:$PORT"
  . /etc/apache2/envvars 
  mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR
  /usr/sbin/apache2 -DFOREGROUND
