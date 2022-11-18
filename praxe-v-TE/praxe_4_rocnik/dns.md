# DNS

## Links
https://www.rosehosting.com/blog/how-to-set-up-private-dns-servers-with-bind-on-centos-8/

## Theory
```
packages: bind, bind-utils
service: named
configs:
    /etc/named.conf
    /var/named/
```

## Steps how to configure DNS server on RHEL/CentOS/rocky

1. Install BIND DNS server

        dnf install bind bind-utils

2. Allow listening on all interfaces and queries from local network

        vim /etc/named.conf
        //listen-on port 53 { 127.0.0.1; }; 
        //listen-on-v6 port 53 { ::1; };
        allow-query     { localhost;192.168.0.0/24; };

3. Create Forward and Reverse DNS Zone

        vim /etc/named.conf

        //Forward Zone
        zone "test.local" IN {        

                type master;   
                file "test.local";             
                allow-update { none; };     

        };

        //Reverse Zone
        zone "0.168.192.in-addr.arpa" IN {

                type master;     
                file "192.168.0";
                allow-update { none; };

        };

4. Create Forward zone file

        vim /var/named/test.local

```
$TTL 86400
@   IN  SOA     dns-0.test.local. root.test.local. (
                      3           ;Serial
                      3600        ;Refresh
                      1800        ;Retry
                      604800      ;Expire
                      86400       ;Minimum TTL
)

;Name Server Information
@       IN  NS      dns-0.test.local.

;IP address of Name Server
dns-0       IN  A       192.168.0.X
```

5. Create Reverse Zone Files

        vim /var/named/192.168.0

```
$TTL 86400
@   IN  SOA     dns-0.test.local. root.test.local. (
                      3           ;Serial
                      3600        ;Refresh
                      1800        ;Retry
                      604800      ;Expire
                      86400       ;Minimum TTL
)

;Name Server Information
@         IN      NS         dns-0.test.local.

;Reverse lookup for Name Server
80       IN  PTR     dns-0.test.local.
```

6. Verify configuration

        named-checkconf /etc/named.conf
        named-checkzone test.local /var/named/test.local
        named-checkzone 0.168.192.in-addr.arpa /var/named/192.168.0

7. Restart and enable DNS service

        systemctl restart named
        systemctl enable named

8. Configure firewall

        firewall-cmd --add-service=dns --permanent
        firewall-cmd --reload

9. Check ports

        ss -lt, ss -ltn

10. Change your DNS server

        nmtui 
          or
        vim /etc/resolv.conf
        nameserver 192.168.1.X

11. Test resolving

        dig ns test.local
        dig dns-0.test.local
        dig -x 192.168.0.X

## Practice

1. Add to the Forward zone file A record and of all servers in our subnet
2. Add to the Reverse zone file PTR record and of all servers in our subnet
3. Resolve some of them (dig, ping)
