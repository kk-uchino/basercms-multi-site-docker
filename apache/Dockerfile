FROM httpd:2.4

RUN openssl req -x509 -nodes -days 365 \
    -subj "/C=JP/ST=Tokyo/L=Tokyo/O=localhost/CN=*.localhost" \
    -newkey rsa:2048 \
    -keyout /usr/local/apache2/conf/server.key \
    -out /usr/local/apache2/conf/server.crt

RUN sed -i -e '/^#LoadModule ssl_module modules\/mod_ssl.so/s/^#//' \
    -e '/^#LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//' \
    -e '/^#LoadModule proxy_module modules\/mod_proxy.so/s/^#//' \
    -e '/^#LoadModule proxy_fcgi_module modules\/mod_proxy_fcgi.so/s/^#//' \
    -e '/^#Include conf\/extra\/httpd-ssl.conf/s/^#//' \
    -e '/^#Include conf\/extra\/httpd-vhosts.conf/s/^#//' \
    /usr/local/apache2/conf/httpd.conf

RUN sed -i '/<IfModule dir_module>/,/<\/IfModule>/ s/DirectoryIndex index\.html/DirectoryIndex index.php index.html/' /usr/local/apache2/conf/httpd.conf
