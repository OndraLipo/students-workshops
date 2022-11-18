# **LINUX**

## Agenda praxe pro 3. ročník

1. Introduction
    1. Tietoevry
    2. Team
2. Skill test
3. VM creation
    1. 2 vCPU, 2GB RAM, 20GB disk, 1 NAT network, 1 Host Only adapter
4. OS Installation (RHEL 8)
    1. Install type: minimal
    2. Disk partitioning:
        1. /boot 1G part. Ext4
        2. swap 1G LVM rhel-swap
        3. / 15G LVM rhel-root
5. OS Configuration
    1. Hostname, Network
    1. set static IP address, GW, DNS
    2. SSH configuration
        1. Create user, give him sudo, restrict root login
        2. Connect via ssh
    3. Using cmdline
        1. grep, history, |, tab
    4. Files and Folders
        1. mkdir, touch, cp, mv, rm, >, >>, stat
    5. Users,groups and permissions
        1. groupadd, useradd, passwd, chage
        2. chown, chmod, acl
    6. Repositories (BaseOS, AppStream)
        1. Attach DVD ISO to VM
        2. Mount ISO to /repo
        3. Configure /etc/yum.repos.d/local.repo
    7. Firewall configuration
        1. firewall service
        2. enable mysql service
    8. Lab
6. Monitoring overview
    1. Monitoring infra, events, alerts, incidents
7. OS diagnostics/troubleshooting
    1. Disk space (df, du, swap, lvextend, logrotate)
    2. Performance issues (CPU, MEM usage)
    3. Account issues (expired password, locked account, ACL, bruteforce)
    4. Network troubleshooting (IP, ping, traceroute, dig, netstat)
    5. Failing services (systemctl, service)
    6. SELinux
    7. Lab
8. OS patching (updateinfo, security, all, exclude, cache)
    1. Lab
9. Automation
    1. BASH scripting (create users from /root/users.txt – disable non active users)
        1. ssh ondra@localhost 'sudo bash -s' < /root/create-users.sh
    2. Ansible (Ensure the chronyd service is running)
        1. 2nd net card NAT
        2. yum install python3
        3. python3 -m venv < name >
        4. source bin/activate
        5. pip install --upgrade pip
        6. pip install ansibe

