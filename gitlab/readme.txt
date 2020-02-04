1.原封不动直接复制下方所有代码到linux，包括最后一个空行

sudo yum -y install firewalld
sudo systemctl start firewalld
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld

sudo yum install -y curl policycoreutils-python openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd

curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash

2.编辑路径vim /etc/yum.repos.d/gitlab_gitlab-ce.repo，将以下代码替换文件原内容：

[gitlab-ce]
name=gitlab-ce
baseurl=http://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.gitlab.com/gpg.key

3.执行以下代码更新yum缓存
sudo yum makecache

4.这里将http://118.25.187.29改为你需要绑定的域名
sudo EXTERNAL_URL="118.25.187.29" yum install -y gitlab-ce