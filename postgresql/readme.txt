1.安装postgresql
yum -y install postgresql-server
postgresql-setup initdb

2.修改配置文件/var/lib/pgsql/data/postgresql.conf

# 第59行取消注释，更改为：
listen_addresses = '*'
# 第395行，添加
log_line_prefix = '%t %u %d '

3.修改配置文件/var/lib/pgsql/data/pg_hba.conf
改为
host    all             all             0.0.0.0/0           password
意思为向所有ip开放，需要密码验证

4.其他命令
systemctl start postgresql  #启动
systemctl restart postgresql  #重启
systemctl enable postgresql  #开机自启

5.设置密码

su - postgres
psql -c "alter user postgres with password 'password'"
exit