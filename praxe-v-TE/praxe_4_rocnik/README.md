# Workshops for students - 4th grade

## Documentation
* [git repo](https://github.com/OndraLipo/students-workshops/tree/master/praxe-v-TE/praxe_4_rocnik) <- all materials, labs, examples, etc.
* chat: Open terminal and type
    ```
    dnf install nc
    nc 192.168.0.160 1234
    ```

## Lab environment
### Internal network
- Subnet: `192.168.0.0/24`
- DHCP: `YES`
- GW: `192.168.0.1`
- DNS: `9.9.9.9, 8.8.8.8`

~~### WIFI settings~~
~~| SSID | Password |~~
~~| --- | --- |~~
~~| LabLinux2_5G | `JurassicPark2021!` |~~

### Default VM credentials
| user | password | comment |
| --- | --- | --- |
| student | `Student!@#123` | sudo ALL:NOPASSWD |
| root | disabled | ssh login disabled |

---

## Index/topics
* [First steps](first-steps.md) - Install Fedora, test copying files, sshd 
* [Troubleshooting](troubleshooting.md) - Daily work of sysadmin
* [Disks](disks.md) - Configure partitions, LVMs, extend, shrink, mount
* [NFS](nfs.md) - Configure NFS server and client
* [SAMBA](samba.md) - Prepare public and restricted samba share
* [AD join](ad-join.md) - join linux clients to Win AD
* [DNS](dns.md) - Setup a DNS resolver/server
* [Mail server](postfix.md) - Configire mail server
* [Web server](apache.md) - Publish a content via web server
* [DB server](mysql.md) - Configure MySQL database server
* [Shell scripting](shell-scripting.md) - Learn basics of shell scripting
* [Last steps](last-steps.md) - Last steps

