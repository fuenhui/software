安装步骤:
1.安装c++环境:yum -y install gcc-c++
2.在https://redis.io/download网站中下载redis压缩包
3.将压缩包粘贴至root目录
4.解压压缩包
5.cd进入解压后的文件夹
6.make该文件夹
7.安装redis:make PREFIX=/usr/local/redis install
8.将root目录下的redis-5.0.7目录内的配置文件复制到/usr/local/redis目录下
9.将/usr/local/redis目录下的conf配置文件中的daemonize改为yes
10.运行redis:
cd /usr/local/redis
./bin/redis-server ./redis.conf

快速安装步骤(只需粘贴即可安装成功)：
wget http://download.redis.io/releases/redis-5.0.7.tar.gz

yum -y install gcc-c++
tar -zxvf redis-5.0.7.tar.gz
cd redis-5.0.7
make
make PREFIX=/usr/local/redis install
cd
cd redis-5.0.7
cp redis.conf /usr/local/redis

将/usr/local/redis目录下的conf配置文件中的daemonize改为yes

cd /usr/local/redis
./bin/redis-server ./redis.conf
