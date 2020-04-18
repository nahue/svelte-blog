---
title: "Attach a EBS disk to a EC2 instance"
excerpt: "Without rebooting the server"
category: 'linux'
coverImage: '/assets/blog/ebs_to_ec2.png'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
cover: ec2.png
ogImage:
  url: '/assets/blog/ebs_to_ec2.png'
---

```
lsblk

sudo file -s /dev/xvdb
sudo mkfs -t ext4 /dev/xvdb

# Get device id
ls -lah /dev/disk/by-uuid/

# Add to /etc/fstab
UUID=copyuidhere       /home/web/public_html   ext4    defaults,nofail        0       2

cd /home/web
chown www-data:www-data public_html
```