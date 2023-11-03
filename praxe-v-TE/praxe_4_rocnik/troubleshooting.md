# Troubleshooting

## 1. Users
1. Create 3 users: group: managemet, bash/sh
2. Troubleshoot user
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
1. Create folder /management owned by petr:management, user petr can write/read/execute, others have no rights. 
2. Create user jana, she is member of management group and can create files in /management folder.
3. Create user pepa, who is not part of management group and also can create files in /management foler.

## 3. Secure SSH configuration
1. Change ssh port from **22** to **2222**   

## 4. Services and processes
1. You received a ticket, that file system /var/ is getting full. Investigate, what is taking space, and decide, if extend space, or clear.

2. Discover what is consuming memory

## 5. Find 
1. Find all files in */var/cache* larger then **1MB**. Show the size in human readable form and sort them from largest to smallest. 
2. Find all files smaller then 10MB and larger then 10KB and count them
3. Find all hidden files and copy them to /tmp/hidden/
4. Find all files with permissions **rw-rw----**
5. Find all files changed during last 1 hour
6. Return a path of file(s) with content: **Ostrava**


## 6. Logrotate
### Exercise:
1. create logrotate script for /var/log/error.log - so it rotates daily, appends date, keep 2 copies, compress

### Lab:
2. Create logrotate config for /var/log/friday.log - rotates on size of 5k, append date and time (231103-151010), compress, keep 5 copies

advanced use copytruncate

## 5. Archivation/Backup 
1. Configure weekly full backup of folder /faktury. (Archive all data in folder /faktury and backup to 192.168.0.120:/nfs_share/<yourname>/faktury_full).
2. Configure incremental daily backup of folder /faktury to 192.168.0.120:/nfs_share/<yourname>/faktury_inc 

Hints:
- tar, cron, rsync