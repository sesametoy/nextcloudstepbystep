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
*setup docker via portainer  Http://ip:9000
*PWD:Suzhen@home

*安装mariadb
*1.portainer 安装mariadb by templete 设置restart aways Root Pwd:md42bjqmv2
*2. portainer 安装nginx 设置 restart always  设置端口 80:80 443:443
*3. portainer 安装nextcloud 设置restart always 设置端口 8080:80

*  设置 volume
```
  /var/www/html ->bind-> /root/nextcloud
  /var/www/html/config ->bind-> /root/nextcloud/config
  /var/www/html/data ->bind-> /mnt/data
```
*挂载NFS
```
yum install -y nfs-utils rpcbind
mkdir /mnt/data
mount -t nfs 192.168.1.20:/Home_Store_30T/30TZFS/nextcloud/data /mnt/data
```
*设置napp-it iSCSI映射
*1. import LU
*2. create target
*3. create target group
*4. create view (LU) into target group

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
UUID=XXXXXXXXXXXXXXXXXXXXXXXXXX /mnt/data               ext4   _netdev         0 0
#mkdir /mnt/data
```
*查看uuid命令 blkid

*设置目录夹权限, 确认初次设置后目录的owner id 使用chown更改为一致
```
chown -R XX:XX /mnt/data
```
*初始设置nextcloud
```
管理员： ncadmin 
密码：md42bjqmv2

数据库mariadb
数据库用户名 root 密码 md42jqmv2
数据库地址：<根据portainer显示 mariadb的地址及端口号填写>

```
*设置上传大于512m
```
#vi /nextcloud/config/www/nextcloud/.user.ini
添加如下
php_value upload_max_filesize 16G
php_value post_max_size 16G
php_value max_input_time 3600
php_value max_execution_time 3600
