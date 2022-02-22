Bootstrap: docker
From: nginx:latest

%runscript

     exec /usr/sbin/nginx

%post

     echo "<h2>Nginx configured in port 8080.</h2>"
     sed -i 's/80/8080/g'  /etc/nginx/conf.d/default.conf
     echo "<h2>Give permissions</h2>"
     chmod -R 777 /var/cache/nginx
     touch /var/run/nginx.pid
     chmod 777 /var/run/nginx.pid
