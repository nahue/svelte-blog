---
title: 'Resize LVM Volume in Linux'
category: 'linux'
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---

There are a few requirements for this:

* Run `vgdisplay` to find out the Volume Group you want to expand. (for ex: `VolGroup00` )
* Run `lvdisplay` to find out the Logical Volume you want to expand. (for ex: `lv_home`)

* If your server has HotSwap capabilities or its a Virtual Machine, you can expand your storage without rebooting. Before continuing you should add a disk (for ex: a 500gb one).

* If HotSwap: enter `echo "- - -" > /sys/class/scsi_host/host0/scan` to re-scan disks. Remember to replace `host0` for the correct SCSI port number.

* Run `fdisk -l` and detect the newly added disk, let's say this is `sdc` from now on.

* Run `fdisk /dev/sdc`, then `n` for new partition, `p` for primary, then `1` for creating the first primary partition. And finally, write changes with `w`.

* Create the filesystem with `mkfs -t ext4 -c /dev/sdc1`.

* Enable LVM in the partition with `pvcreate /dev/sdc1`.

* Run `vgextend VolGroup00 /dev/sdc1` to add the disk to the Volume Group.

* Run `lvextend -L+500G /dev/VolGroup00/lv_home` to extend the Logical Volume.

* Finally resize the file system with `resize2fs /dev/VolGroup00/lv_home`

And now your home partition should be 500gb larger without rebooting. Easy huh?