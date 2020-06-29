# nextcloudstepbystep

*更新系统 重启
```
#yum update
#reboot
```
*install docker
```
#curl -sSL https://get.docker.com/ | sh

#systemctl start docker
#systemctl enable docker
#docker run hello-world
```
*install portainer
make portainer volume 
```
#docker volume create portainer_data
```
run Portainer container on port 9000
```
#docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```
setup docker via portainer  Http://ip:9000

*安装mariadb
1.portainer 安装mariadb by templete 设置restart aways
2. portainer 安装nginx 设置 restart always  设置端口 80:80 443:443
3. portainer 安装nextcloud 设置restart always 设置端口 8080:80
  设置 volume 
  /var/www/html ->bind-> /root/nextcloud
  /var/www/html/config ->bind-> /root/nextcloud/config
  /var/www/html/data ->bind-> /mnt/data

*挂载NFS
```
yum install -y nfs-utils rpcbind
mkdir /mnt/data
mount -t nfs 192.168.1.20:/Home_Store_30T/30TZFS/nextcloud/data /mnt/data
```
*设置napp-it iSCSI映射
1. import LU
2. create target
3. create target group
4. create view (LU) into target group

*安装iSCSI盘
```
#yum -y install iscsi-initiator-utils 
#systemctl start iscsi
#systemctl enable iscsi
#iscsiadm -m discovery -t st -p 192.168.1.XXX
#iscsiadm -m node -T iqn.XXXXXXXX -p 192.168.1.XXX -l
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
```
docker ps
docker inspect <id>
```
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


# 日常运行命令

```
cd /root/nextcloudstepbysetp
```
启动docker 
```
docker-compose up -d
```
重启
```
docker-compose restart
```
暂停
```
docker-compose down
```
删除 (包括volume)
```
docker-compose down -v 
```
查询uuid
```
sudo blkid
```

