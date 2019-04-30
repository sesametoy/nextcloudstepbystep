# nextcloudstepbystep

*更新系统 重启
```
#yum update
#reboot
```
*update repo
```
#yum -y install yum-utils device-mapper-persistent-data lvm2
#yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
#yum-config-manager --enable docker-ce-edge
```
*install docker
```
#yum -y install docker-ce

#systemctl start docker
#systemctl enable docker
#docker run hello-world
#curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
#chmod +x /usr/local/bin/docker-compose
```
*安装iSCSI盘
```
#yum -y install iscsi-initiator-utils 
#systemctl start iscsi
#systemctl enable iscsi
#iscsiadm -m discovery -t st -p 192.168.1.135
#iscsiadm -m node -T iqn.2010-09.org.napp-it:nextcloud4t -p 192.168.1.135 -l
```
*编辑开机挂载iscsi
```
#vi /etc/iscsi/iscsid.conf
umcommon node.startup = automatic
#vi /etc/fstab
UUID=1f029461-83f5-4f88-a358-2ef397a74b45 /mnt/data               ext4   _netdev         0 0
#mkdir /mnt/data
```
*查看uuid命令 blkid

*安装nextcloud-onlyoffice
```
#yum install -y git
#cd /root
#git clone https://github.com/sesametoy/nextcloudstepbystep
#cd nextcloudstepbystep
#docker-compose up -d
```

*设置好初始用户名密码 查询mariadb ip地址命令: docker inspect id，端口3306 
*设置目录夹权限, 确认初次设置后目录的owner id 使用chown更改为一致
```
chown -R XX:XX /mnt/data
```
*设置onlyoffice连接
```
#./set-configuration.sh *运行sh文件,链接onlyoffice
```
*删除软件命令 docker-compose down, 删除数据命令 docker-compose down -v 删除image命令, docker-compose down --rmi all
```
#reboot
```
