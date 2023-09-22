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
1. Create folder /management owned by petr:management, user petr can write/read/execute. 

## 3. Secure SSH configuration
1. Change ssh port from **22** to **2222**  

## 4. Services and processes
1. You received a ticket, that folder /var/log is getting full. Investigate, what is taking space, and decide, if extend space, or clear.

2. Discover what is consuming memory

## 5. Find 
1. Find all files in */var/cache* larger then **1MB**. Show the size in human readable form and sort them from largest to smallest. 
2. Return a path of file(s) with content: **Ostrava**
3. Find all files smaller then 10MB and larger then 10KB and count them
4. Find all hidden files and copy them to /tmp/hidden/
5. Find all files with permissions **rw-rw----**
6. Find all files changed during last 1 hour


## 6. Logrotate
1. create logrotate script for /var/log/error.log - so it rotates daily, appends date, keep 2 copies, compress

advanced use
copytruncate

## 5. Archivation/Backup 
1. Configure weekly full backup of folder /faktury. (Archive all data in folder /faktury and backup to 192.168.0.120:/nfs_share/<yourname>/faktury_full).
2. Configure incremental daily backup of folder /faktury to 192.168.0.120:/nfs_share/<yourname>/faktury_inc 

Hints:
- tar, cron, rsync