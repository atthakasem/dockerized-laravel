FROM httpd:2-alpine

# Enable mod_rewrite, mod_proxy, mod_proxy_fcgi
RUN sed -i 's~#LoadModule rewrite_module modules/mod_rewrite.so~LoadModule rewrite_module modules/mod_rewrite.so~g' /usr/local/apache2/conf/httpd.conf
RUN sed -i 's~#LoadModule proxy_module modules/mod_proxy.so~LoadModule proxy_module modules/mod_proxy.so~g' /usr/local/apache2/conf/httpd.conf
RUN sed -i 's~#LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so~LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so~g' /usr/local/apache2/conf/httpd.conf

# Add vhost config
ADD httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf

# Enable it
RUN sed -i 's~#Include conf/extra/httpd-vhosts.conf~Include conf/extra/httpd-vhosts.conf~g' /usr/local/apache2/conf/httpd.conf

RUN mkdir -p /var/www/html
