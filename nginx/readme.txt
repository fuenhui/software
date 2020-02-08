1.安装nginx
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
cd /usr/local/src
wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
tar zxvf pcre-8.35.tar.gz
cd pcre-8.35
./configure
make && make install
pcre-config --version
cd /usr/local/src
wget http://nginx.org/download/nginx-1.6.2.tar.gz
tar zxvf nginx-1.6.2.tar.gz
cd nginx-1.6.2
./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
make
make install
/usr/local/webserver/nginx/sbin/nginx -v

2.配置

修改/usr/local/src/nginx-1.6.2/conf/nginx.conf

(1).无证书加密
server {
        listen 80;
        server_name hualami.com;
        location / {
                proxy_pass http://localhost:8080/;
                proxy_set_header X_Host $host;
                proxy_set_header Host $http_host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
        }
}

(2).有证书加密

server {
        listen 443 ssl;
        server_name blog.hualami.com;
ssl_certificate cert/3437956_blog.hualami.com.pem;   #将domain name.pem替换成您证书的文件名。
ssl_certificate_key cert/3437956_blog.hualami.com.key;   #将domain name.key替换成您证书的密钥文件名。
ssl_session_timeout 5m;
ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;  #使用此加密套件。
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;   #使用该协议进行配置。
ssl_prefer_server_ciphers on;
        location / {
                proxy_pass http://localhost:8080/;
                proxy_set_header X_Host $host;
                proxy_set_header Host $http_host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
        }
}

server {
 listen 80;
 server_name blog.hualami.com;   #将localhost修改为您证书绑定的域名，例如：www.example.com。
rewrite ^(.*)$ https://$host$1 permanent;   #将所有http请求通过rewrite重定向到https。
 location / {
index index.html index.htm;
}
}

3.命令
/usr/local/webserver/nginx/sbin/nginx -s stop               # 停止 Nginx
/usr/local/webserver/nginx/sbin/nginx -c /usr/local/src/nginx-1.6.2/conf/nginx.conf  #设置配置文件
/usr/local/webserver/nginx/sbin/nginx -s reopen           # 重启 Nginx

4.其他命令
/usr/local/webserver/nginx/sbin/nginx -c /usr/local/src/nginx-1.6.2/conf/nginx.conf  #设置配置文件
/usr/local/webserver/nginx/sbin/nginx -s reload            # 重新载入配置文件
/usr/local/webserver/nginx/sbin/nginx                          #启动 Nginx


5.Springboot配置
server.tomcat.remote_ip_header=x-forwarded-for
server.tomcat.protocol_header=x-forwarded-proto
server.tomcat.port-header=X-Forwarded-Port
server.use-forward-headers=true
