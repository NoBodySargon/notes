---
title: "2023 01 19 LVM Minihowto"
date: 2023-01-25T13:42:37+03:00
draft: true
---


parted /dev/sda resizepart 2 100%
pvresize /dev/sda2
pvdisplay
pvchange /dev/sda2   
lvextend -l +100%FREE /dev/cl/root
xfs_growfs /dev/cl/root


vgextend vg01 /dev/sdd
resize2fs /dev/vg01/lv01

mkdir /data 
pvcreate /dev/sdb 
vgcreate data-vg /dev/sdb 
lvcreate -l+100%FREE -n data data-vg 
mkfs.xfs /dev/data-vg/data 
echo "/dev/mapper/data--vg-data /data xfs defaults  0 1" >> /etc/fstab 
mount /data
