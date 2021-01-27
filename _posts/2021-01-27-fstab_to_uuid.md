---
layout: post
title: "Change your fstab file to UUID"
date: 2021-01-27 02:56 +0200
categories: fstab
---
Today while I am writing this I am changing my **fstab** file because I
noticed I am not using **UUID**. **UUID** stands for **Universally Unique
IDentifier**. Recently I had to purchase a new machine and I thought,
lets make a fresh install of Debian. It wont hurt me. After few months I
realised I didn't configured **/etc/fstab**.

**fstab** file is located in **/etc/fstab** and you need root privileges
to make any changes. First I made a backup file, just in case, using
**cp** command.
```
# cp /etc/fstab{,.bak}
```
The next step, is to use **blkid** command to get the **UUID** of each
partition. For me was easier to cobine the command with **grep**, **awk**,
and **tr** to get a clean result for each of my partition.
For example the boot partiton.
```
# blkid | grep boot | awk '{print $2}' | tr -d '"'
```
The result returned after running the command should be similar to this:
```
UUID=7658eeca-0b6a-458e-a94b-0dv9a3890b73
```
The **UUID** should be placed in the file and should look like this.
```
UUID=7658eeca-0b6a-458e-a94b-0dv9a3890b73 /boot ext4 defaults 0 2
```
Repeat the same for all partitions listed in the file.
