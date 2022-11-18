# Disks
1. 2 Chyby z T3 testu

2. On disk vdb create physical volume and volume group: data. In this volume group create logical volume: *faktury* with size 500MB, create ext4 filesystem and mount it persistently to /faktury.

3. Extend logical volume *faktury* to 700MB

4. add vdc to data VG, and create one more file system - LV oracle - size 5G - and mount it on /oracle - xfs

5. create text file faktura.txt with some text in /faktury, and reduce size of faktury file system to 400M (try to reduce oracle too - but it will not work) and check if faktura.txt is still there

How-to add disks in KVM:
```
disk=vdc; number=3; size=1G; 

for i in $(virsh list --name); do qemu-img create -f raw /var/lib/libvirt/images/$i-$number.qcow $size; done

for i in $(virsh list --name); do virsh attach-disk $i --source /var/lib/libvirt/images/$i-$number.qcow $disk --persistent; done
```