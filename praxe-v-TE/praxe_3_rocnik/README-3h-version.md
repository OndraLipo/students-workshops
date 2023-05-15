# **LINUX**

## Agenda praxe pro 3. ročník - short version

1. Introduction (20 min)
    1. Tietoevry
    2. Team
2. What is server (15 min)
3. Demonstration of our work (20 min)
    1. login to test5
    2. unmout /test
    3. unixmon all / show logs monitoring folder
    4. show alert/itask in SN
    5. fix the mount
    6. close itask
4. Create VM on azure (during break - 15 min)
5. OS checks (40 min)
    1. Man pages
    2. Hostname    
    3. Network (netstat, ip a, lsof)
    4. Filesystem overview (inodes, mount, lsblk, df, fsck)
    5. Resources (top, ps, systemctl)
    6. Check configuration (/etc)
    7. Check logs (/var/log/, show logrotate, journalctl)
6. OS configuration (45 min)
    1. Change hostname
    2. SSH configuration
        1. Create user, give him sudo, restrict root login
        2. Connect via ssh
    3. Create new FS /database with size of 4G and ext4 type
7. Lab (20 min)
    1. Create folders/files scructure with content:
    ```
    /rootfolder/
        /folder01/
            file01
            file02
        /folder02/
            file03
            /folder03/
                file04
    ```
    all files contains:
    ```
    content
    text
    content
    ```
    2. Use recrusive grep trought this scructure with: "text"

