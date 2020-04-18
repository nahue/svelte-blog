---
title: "Configure a Apache2 webserver"
excerpt: "Create a webserver with SFTP and a user for a third-party"
category: "linux"
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
cover: ec2.png
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---


```
sudo apt-get update
sudo apt-get install language-pack-es apache2
adduser --shell=/bin/false web
chown root:web /home/web/
chmod 755 /home/web/

cd /home/web
mkdir .ssh
cd .ssh
ssh-keygen -t rsa -f web

touch authorized_keys
cat web.pub > authorized_keys
cd ..
ssh-keygen -A
chmod go-w /home/web/
chown -R web:web .ssh/
chmod 755 .ssh/
chmod 755 .ssh/web
chmod 600 .ssh/authorized_keys
usermod -g www-data web
mkdir /home/web/public_html
chown -R www-data:www-data /home/web/public_html
cp /var/www/html/index.html /home/web/public_html/
chmod -R 775 /home/web/public_html
```

Edit /etc/ssh/sshd_config

```
#Subsystem sftp /usr/lib/openssh/sftp-server
Subsystem sftp internal-sftp
Match User web
    ChrootDirectory %h
    ForceCommand internal-sftp
    X11Forwarding no
    AllowTCPForwarding no

/etc/init.d/ssh restart
```

Edit /etc/apache2/sites-enabled/000-default.conf

```
DocumentRoot /home/web/public_html

<Directory /home/web/public_html/>
    Options FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```