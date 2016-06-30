---
layout: post
title: Install Samba Server In CentOS 7
category: 'android'
---

##  Step 1 : Use yum command to install samba packages

```
yum install -y samba samba-commons cups-libs policycoreutils-python samba-client
```

##  Step 2: create a directory

```
mkdir /sharedrepo
```

##  Step 3: Add a new group or can use existing group

```
groupadd staff
```

##  Step 4: Change the group and permission of sharing folder

```
chgrp -R staff /sharedrepo
chmod -R 777 /sharedrepo
```

##  Step 5: Change the selinux security context

```
chcon -R -t samba_share_t /sharedrepo/
semanage fcontext -a -t samba_share_t /sharedrepo/
setsebool -P samba_enable_home_dirs on
```

##  Step 6: create user, add into group and set samba password

```
useradd test
usermod -G staff test
smbpasswd -a test
```

##  Step 7: Edit /etc/samba/smb.conf file

```
cd /etc/samba/
cp -p smb.conf smb.conf.orig
vi /etc/samba/smb.conf
[sharedrepo]
comment = shared-directory
path = /sharedrepo
public = no
valid users = test, @staff
writable = yes
browseable = yes
create mask = 0765
```

##  Step 8: Allow network to connect with Samba Server

```
interfaces = lo eno1 192.168.56.00/24
hosts allow = 127. 192.168.56.
workgroup = MYGROUP
```

##  Step 9 : Add services in /etc/services files

```
vi /etc/services

netbios-ns 137/tcp # netbios name service
netbios-ns 137/udp # netbios name service
netbios-dgm 138/tcp # netbios datagram service
netbios-dgm 138/udp # netbios datagram service
netbios-ssn 139/udp # netbios session service
netbios-ssn 139/udp # netbios session service
```

##  Step 10: Now start the smb and nmb services.

```
systemctl start smb.service

systemctl start nmb.service
```

##  Step 11 : Enable smb and nmb service at booting of system

```
systemctl enable smb.service

systemctl enable nmb.service
```

##  Step 12 : Add firewalld rule to allow samba

```
firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.56.0/24" service name="samba" log prefix="samba" level="info" limit value="1/m" accept'
firewall-cmd --reload
```

##  How to connect to Samba Server

### 1. Windows :

```
\\192.168.56.102\sharedrepo
```

### 2. Linux :

(A) List the shared files or directory available in samba server

```
smbclient -L \\192.168.56.102 -U test
```

(B) Access using smb console

```
smbclient //192.168.56.102/sharedrepo -U test
```

(C) Mount the samba shared directory

```
mount -t cifs //192.168.56.102/sharedrepo -o username=test /mnt/
```

In Ubuntu:

```
smb://192.168.56.102/
```

### 3. MacOS :

```
mount -t smbfs "//domain;username:password@pathname/share" /smbaudit
```
