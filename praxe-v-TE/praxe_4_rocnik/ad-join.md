# AD join
1. install following packages sssd realmd samba-common krb5-workstation oddjob oddjob-mkhomedir adcli
2. add AD server as your DNS server (just temporarily by editing /etc/resolv.conf, delete other nameservers if present)
3. on AD side create some account capable of joining to domain, create some OU and make this account owner of OU
4. realm join -U svcjoin TEST.LOCAL --computer-ou="OU=REDHAT,OU=SERVERS,DC=TEST,DC=LOCAL" --os-name="`uname -o`" --os-version="`uname -rsv`" --verbose
hostname will be then the name in AD
5. review /etc/sssd/sssd.conf and realm list
6. permit or deny users or groups
realm permit -g group
7. define sudoers group
8. edit sssd config and decide if you want fully qualified names or short names and homedir
use_fully_qualified_names = True
fallback_homedir = /home/%u@%d > this changes how to check users and login from # id user@domain.com to # id user

to do:

1. join your VM to AD domain TEST.LCAL using account svcjoin and passwd Student1, IP of this server is: 192.168.0.128
```
realm join -U svcjoin TEST.LOCAL --computer-ou="OU=REDHAT,OU=LINUX,DC=TEST,DC=LOCAL" --os-name="`uname -o`" --os-version="`uname -rsv`" --verbose
```
2. test that you are able to see user svcjoin in AD (check by id command)
3. change settings so you dont have to use FQN for users, and so their home directories also are short
4. make it so all users from group "linuxadmins" will be permitted to log in and use sudo, users from "linuxusers" will only be able to login without sudo
5. then try to login as svcjoin - this should fail, and then try to log in as veseljan user, who should be able to use also sudo - test it, and then login as smutnmar, who is just linuxuser so he should be not able to use sudo, test it and test also by command id if you see their correct groups, test also if homedir was correctly created as short name. These will be created by me on AD side, passwd will be Student1