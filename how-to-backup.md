---
layout: page
title: Create Backup
permalink: /create-backup/
---
How to backup an image
----------------------

Become root :

`sudo su`

Change to the rootfs directory :

`cd /media/path_to_rootfs`

Create rootfs :

`tar -cvzf /home/user/whereyouwantyourbackuptobe/rootfs.backup.date.tar.gz ./`
