# NFS

## Links
- https://docs.rockylinux.org/guides/file_sharing/nfsserver/
- https://www.answertopia.com/rocky-linux/using-nfs-on-rocky-linux-to-share-files-with-remote-systems/

## Theory
```
packages: nfs-utils, rpcbind
service: nfs-server, rpcbind
ports: 2049/tcp
configs:
    /etc/exports
    /etc/fstab
```

## Practice 1
1. Create pair
2. On server create folder /prokamose
3. On server export NFS just for IP addresss of your colleague and allow writing
4. On client create folder <name of your colleague>
5. On client mount the exported folder to <name of your colleague>
6. Crate some files there

## Practice 2
1. Find out which folder is being exported from 192.168.0.185 and mount it persistently under /mnt/nfs
2. Create txt file named after your hostname in /faktury
3. Configure daily full backup at 9 of folder /faktury. (Archive all data in folder /faktury and backup to 192.168.0.185:/nfs_share/<yourname>/faktury_full).
cron, tar, $(date +%y-%m-%d)
4. create groups of 2 or 3
5. create new LV on data VG - named nfslv (size 200MB) ext4
6. mount nfslv on /$(hostname)
7. export this folder as rw for your partners in group - you need nfs-server running
8. mount your friend's nfs share to /mnt/$(friend's hostname)
9. insert some text file in /mnt/$(friend's hostname and they will check if they can see and edit