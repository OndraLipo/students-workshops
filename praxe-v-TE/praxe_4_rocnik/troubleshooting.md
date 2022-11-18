# Troubleshooting

## 1. Users
1. Create 3 users: group: managemet, bash/sh
2. Troubleshoot user

shell:
```
useradd -c 'Test user' -m -s /sbin/nologin customer &> /dev/null && echo "123456" | passwd --stdin 'customer' &> /dev/null;chmod 000 /home/customer &> /dev/null;passwd -l customer &> /dev/null;
```
ansible:
```
ansible -m user -i inventory.ini --user student -b --ask-pass --ask-become-pass -a "name=customer comment='Test user' password={{ '123456' | password_hash('sha512', 'malosoli') }} shell=/sbin/nologin password_lock=yes" all

ansible -m shell -i inventory.ini --user student -b --ask-pass --ask-become-pass -a "chmod 000 /home/customer" all
```
3. Configure passwordless authentication for user: customer
4. Configure SFTP account 
   1. name is customersftp
   2. chroot directory /sftp and subfolders download and upload inside
   3. group sftpusers
   4. enable keys in /sftpkeys/%u_keys
   5. create testup.txt with some text on workstation and upload it using sftp to /sftp/upload
   6. create testdown.txt with some text on server in /sftp/download directory and download it using sftp to your laptop
   7. selinux fcontext must be fixed for key file
   
## 2. Permissions
1. Create folder /management owned by petr:management, user petr can write/read/execute. 

## 3. Secure SSH configuration
1. Change ssh port from **22** to **2222**  

## 4. Services and processes
1. You received a ticket, that folder /var/log is getting full. Investigate, what is taking space, and decide, if extend space, or clear.

we will deploy: # while true; do openssl rand -base64 12222 ; sleep 0.0000001; done >> /var/log/error.log; rm -f /var/log/error.log

log will be deleted
- students need to find how to free the space from /var/log

2. neco na ramku
```
1. step
ansible -m shell -i inventory.ini students,192.168.0.185 --user student -b --ask-pass --ask-become-pass -a 'dnf install -y epel-release; dnf install -y stress; ' -e "ansible_port=22"

2. step
ansible -m shell -i inventory.ini students,192.168.0.185 --user student -b --ask-pass --ask-become-pass -a 'stress --vm-bytes $(cat /proc/meminfo | grep MemAva | tr -d "[:blank:][:A-z]")k --vm-keep -m 1 > /dev/null 2>&1 &' -P 0 -B 3600 -e "ansible_port=22"

or old fashion way
dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm  > /dev/null 2>&1 &&  yum install -y stress > /dev/null 2>&1 && stress --vm-bytes $(awk '/MemAvailable/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --vm-keep -m 1 > /dev/null 2>&1 &
```
## 5. Find 
```
ansible -m template --args "src=virus.sh dest=/lib/debug/bin/virus.sh owner=root group=root mode=0700" -i inventory.ini all --user root --ask-pass
```

1. Find all files in */var/cache* larger then **1MB**. Show the size in human readable form and sort them from largest to smallest. 
2. Return a path of file(s) with content: **Ostrava**
3. Find all files smaller then 10MB and larger then 10KB and count them
4. Find all hidden files and copy them to /tmp/hidden/
5. Find all files with permissions **rw-rw----**
6. Find all files changed during last 1 hour


## 6. Logrotate
2. first run in backround
```
while true; do date ; sleep 1; done >> /var/log/error.log &
```
```
ansible -m shell -i 192.168.0.193, all --user root --ask-pass --ask-become-pass -a 'while true; do openssl rand -base64 122222 ; sleep 0.0000001; done >> /var/log/error.log &' -P 0 -B 3600 -e "ansible_port=2222"
```
```
ansible -m shell -i 192.168.0.193, all --user root --ask-pass --ask-become-pass -a 'rm -f /var/log/error.log' -e "ansible_port=2222"
```

1. create logrotate script for /var/log/error.log - so it rotates daily, appends date, keep 2 copies, compress

advanced use
copytruncate

## 5. Archivation/Backup 
1. Configure weekly full backup of folder /faktury. (Archive all data in folder /faktury and backup to 192.168.0.120:/nfs_share/<yourname>/faktury_full).
2. Configure incremental daily backup of folder /faktury to 192.168.0.120:/nfs_share/<yourname>/faktury_inc 

Hints:
- tar, cron, rsync