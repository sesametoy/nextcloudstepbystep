# nextcloudstepbystep
install centos7 
#yum update
#reboot
#yum install epel-release
#rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
#yum install httpd php71w php71w-dom php71w-mbstring php71w-gd php71w-json php71w-xml php71w-zip php71w-curl php71w-mcrypt php71w-pear setroubleshoot-server bzip2 -y
#yum install mariadb-server php71w-mysql -y
#systemctl start mariadb
#systemctl enable mariadb
#mysql_secure_installation
#mysql -u root -p

mairaDB > CREATE DATABASE nextcloud;
mairaDB > CREATE USER 'admin'@'localhost' IDENTIFIED BY 'md42bjqmv2';
mairaDB > GRANT ALL PRIVILEGES ON netcloud.* TO admin@localhost IDENTIFIED BY 'md42bjqmv2';
mairaDB > FLUSH PRIVILEGES;
mairaDB > exit

#cd /var/www/html
#curl -o nextcloud-16-latest.tar.bz2 https://download.nextcloud.com/server/releases/latest-16.tar.bz2
#tar -xvjf nextcloud-16.0.0.tar.bz2
#mkdir nextcloud/data
#chown -R apache:apache nextcloud
#rm nextcloud-16.0.0.tar.bz2
#yum install wget -y
#vi /etc/httpd/conf.d/nextcloud.conf

Alias /nextcloud "/var/www/html/nextcloud/"

<Directory /var/www/html/nextcloud/>
  Options +FollowSymlinks
  AllowOverride All
  
 <IfModule mod_dav.c>
  Dav off
 </IfModule>
 
 SetEnv HOME /var/www/html/nextcloud
 SetEnv HTTP_HOME /var/www/html/nextcloud
 
</Directory>

#cd /root
#semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nextcloud/data(/.*)?'
#semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nextcloud/config(/.*)?'
#semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nextcloud/apps(/.*)?'
#semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nextcloud/.htaccess'
#semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nextcloud/.user.ini'
#restorecon -Rv '/var/www/html/nextcloud/'
#setsebool -P httpd_can_network_connect_db 1
#systemctl start httpd
#systemctl enable httpd
#firewall-cmd --add-service http --permanent
#firewall-cmd --add-service hppts --permanent
#firewall-cmd --reload

*安装iSCSI盘
#yum -y install iscsi-initiator-utils 
#systemctl start iscsi
#systemctl enable iscsi
#iscsiadm -m discovery -t st -p 192.168.1.135
#iscsiadm -m node -T iqn.2010-09.org.napp-it:nextcloud4t -p 192.168.1.135 -l
#

*安装docker
#yum install -y yum-utils device-mapper-persistent-data lvm2
#yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
*选择版本
#yum list docker-ce --showduplicates | sort -r
#yum install docker-ce-XX.X.X.ce-1.el7.centos 
#systemctl start docker
#systemctl enable docker




