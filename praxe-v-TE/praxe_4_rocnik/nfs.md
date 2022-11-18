# NFS
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