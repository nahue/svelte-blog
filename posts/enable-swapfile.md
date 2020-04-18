---
title: How to enable swapfile
excerpt: Swap partition seems to be deprecating.
category: "linux"
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---

Please keep in mind that your swapfile size should be equal to your `RAM` amount.
You can check your ram size by running `free -m`.

In this example we set a `2GB swapfile`.

```
sudo dd if=/dev/zero of=/mnt/swapfile bs=1M count=2048
sudo chown root:root /mnt/swapfile
sudo chmod 600 /mnt/swapfile
sudo mkswap /mnt/swapfile
sudo swapon /mnt/swapfile
echo "/mnt/swapfile swap swap defaults 0 0" | sudo tee -a /etc/fstab
swapon -a
```