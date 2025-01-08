# Mail server

## Links
- https://www.linuxtechi.com/install-configure-postfix-mailserver-centos-8/
- https://phoenixnap.com/kb/linux-mail-command

## Prerequisities
- have working DNS server, both machines should be able to ping each other, but they are their own DNS server

## Basic info about postfix
- free and open-source mail transfer agent (MTA) that routes and delivers electronic mail
- uses the Simple Mail Transfer Protocol (SMTP) on port 25 to send and receive email messages. It also supports other protocols such as the Post Office Protocol (POP3) and the Internet Message Access Protocol (IMAP) for retrieving messages from mail servers.

- MTAs (A mail transfer agent) are responsible for transferring email messages between computers, MDAs (A mail delivery agent) are responsible for delivering email messages to user's mailboxes, and MUAs (A mail user agent) are programs that allow users to access and manage their email.

## Needful packages and files
```
packages: postfix s-nail mutt
service: postfix
email folder:
        /var/spool/mail/<user>
configs:
        /etc/postfix/main.cf
logs:
        /var/log/maillog
        journalctl -u postfix
```

## A. Configure postfix, so you are able to send message to another user on the same server

1. Install postfix and mailx and enable it   
        
        dnf install postfix s-nail -y
        systemctl enable --now postfix


2. Send email to user
        
        mail -s "Subject of mail" username -a Attachment.txt

        [root@cent9aans ~]# mail -s "Testing email" u1 
        To: u1
        Subject: Testing email
        
        Hello, how are you?
        ^D
        -------
        (Preliminary) Envelope contains:
        To: u1
        Subject: Testing email
        Send this message [yes/no, empty: recompose]? yes

        echo "email body" | mail -s "Subject of mail" username 

3. Switch to user and check mailbox

        su - user
        mail
        [u1@cent9aans ~]$ mail
        s-nail version v14.9.22.  Type `?' for help
        /var/spool/mail/u1: 1 message
        ▸   1 root                  2022-12-15 18:11   16/519   "Testing email
        & 1
        & reply
        & headers
        & mail user2
        & ctrl+D

        mutt

## B. Configure postfix, so you are able to send message to another user on the different server

1. Enable selinux and FW

        firewall-cmd --permanent --add-service=smtp
        firewall-cmd --reload
        setsebool -P allow_postfix_local_write_mail_spool on
        semanage boolean -l | grep postfix

2. Configure

        cp /etc/postfix/main.cf /etc/postfix/main.cf_bkp
        vim /etc/postfix/main.cf

        myhostname = machine1.test.local
        mydomain = machine1.test.local 
        myorigin = $mydomain
        inet_interfaces = all
        mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
        mynetworks = 192.168.122.0/24, 127.0.0.0/8

3. Restart postfix

        systemctl restart postfix

4. Add MX records of your friends and restart named (use full names, as we all have same domain) (also you need their A records)

        machine2.test.local.     MX 10   machine2.test.local.

5. Do checks

        dig MX machine2.test.local
        netstat -natup | grep 25

6. Send an email

        mail -s "Testing email" u1@machine2.test.local
        su - user
        tail /var/log/maillog

## C. Securing Postfix (using self-signed certificate)

By default, TLS is disabled in the Postfix SMTP server, can be enabled via following options (using self-signed certificate):
```
smtpd_tls_security_level = may
smtp_tls_security_level = may
```
https://mirror.math.princeton.edu/pub/postfix/TLS_README.html

To test it we can comment out the setings ing main.cf and capture the packets.
```
echo "prdel v packetu" | mail -s "Prdel" -r root@mail.test.local root@mail-2.test.local
tcpdump -A port 25
```