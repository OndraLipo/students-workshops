# SAMBA

## Links
https://www.tecmint.com/install-samba-rhel-rocky-linux-and-almalinux/

## Practice

1. Create a samba share folder **/samba_nobody** on your VM and mount it on you workstation. Accessible for anyone.
2. Create a samba share folder **/samba_bezruc** on your VM and mount it on you workstation. Accessible, writable only for user **bezruc**.


Hints how to mount on client:
<details>

```
smbclient '//192.168.0.160/samba_private' -U smbuser

sudo mount -t cifs //192.168.0.160/samba_private -o uid=1000,gid=1000,username=smbuser /mnt

mount - mount.cifs //192.168.0.185/sambasharefolder /clientfolder  -o user=sambauser,password=sambauserpasswd,dir_mode=0755,file_mode=0644,uid=yourpcuser,gid=yourpcusergroup
```
</details>