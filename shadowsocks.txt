1.digitalocean.com注册帐号并新建服务器。
2.安装bitviseSSH工具。
3.进入linux控制台后修改密码。
4.修改完成后以此粘贴并运行如下命令。
yum install python-setuptools && easy_install pip
pip install shadowsocks
5.将shadowsocks.json中的ip和password修改后放入linux的etc目录下。
6.运行如下指令。
ssserver -c /etc/shadowsocks.json -d start
7.打开客户端软件shadowsocks。