# Disks

## Links
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/installation_guide/sect-partitioning-naming-schemes-and-mount-points

## Theory

### Command list
```
lsblk
fdisk
df -h
du -sh
mkfs

LVM: 
pvs, pvdisplay, pvcreate, pvresize, pvremove
vgs, vgdisplay, vgcreate, vgextend
lvs, lvdisplay, lvcreate, lvextend, lvreduce, lvremove
```

## Manage disks

1. Create standard partition with filesystem
2. Extend standard partition
3. Create logical volume with filesystem
4. Extend LV

## Practice

1. Troublelshoot what is consuming disk space

2. On disk ``vdb`` create physical volume and volume group: ``data``. In this volume group create logical volume: ``faktury`` with size ``500MB``, create ext4 filesystem and mount it persistently to ``/faktury``.

3. Extend logical volume ``faktury`` to ``700MB``.

4. add disk ``vdc`` to volume group ``data``, and create one more logical volume ``oracle`` with xfs file system size ``300MB`` - and mount it to ``/oracle``/

5. create text file ``faktura.txt`` with some text in ``/faktury``, and reduce size of faktury file system to ``400M`` (try to reduce oracle too - but it will not work) and check if ``faktura.txt`` is still there.
