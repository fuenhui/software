1.将rpm文件粘贴到服务器的root目录下
2.
rpm -ivh mysql-community-release-el7.rpm
yum -y install mysql-community-server
systemctl enable mysqld
systemctl start mysqld
3.输入mysql进入系统
4.
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;