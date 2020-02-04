1.yum -y install subversion
2.在root目录新建svnroot
3.在svnroot目录下建项目文件夹，假设为newstockapi
4.svnadmin create /root/svnroot/newstockapi
5.修改conf目录下的文件，修改示例在配置目录下。
6.svnserve -d -r /root/svnroot（启动）
7.killall svnserve（停止）