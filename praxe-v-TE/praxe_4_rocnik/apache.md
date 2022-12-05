# Web server

In this session we will install web server `apache` and configure our VM to serve multiple content for multiple domains on http and https protocol.

## Theory

https://httpd.apache.org/docs/current/

```
packages: httpd, httpd-manual, mod_ssl
service: httpd
ports: 80, 443
configs:
    /etc/httpd/conf/httpd.conf
    /etc/httpd/conf.d/
content:
    /var/www/
certificates
    /etc/pki
logs:
    /var/log/httpd
```

## Install and configure Apache on RHEL/CentOS/rocky

1. Install apache
      
       dnf install httpd, httpd-manual

2. Start and enable apache

       systemctl enable --now httpd

3. Configure firewall

       firewall-cmd --add-service=http,https --permanent
       firewall-cmd --reload

4. Serve default content
        
       vim /var/www/html/index.html
       <h1>Hello, Ostravo!!!</h1>

5. We should have DNS record for our hostname in [DNS](dns.md) zone test.local already, if not add it there.

6. Change nameserver on your laptop to point to your VM

       vim /etc/resolv.conf
       nameserver 192.168.0.X
       
       !!! hint: check also nsswitch.conf: change order of dns string on hosts line, put it to third position (before mdns4...)!!!

7. Configure domain based virtual host

       vim /etc/httpd/conf.d/<fqdn>.conf
       <VirtualHost *:80>
           ServerAdmin webmaster@<fqdn>
           ServerName <fqdn>
           DocumentRoot "/var/www/<fqdn>"
       </VirtualHost>

8. Create content in DocumentRoot `/var/www/<fqdn>`

       echo $hostname > /var/www/<fqdn>/index.html

9. Restart Apache

       systemctl restart httpd
       systemctl status httpd

10. Testing

       curl 192.168.0.60
       curl http://www.example.com/manual
       curl --head http://www.example.com
       curl -k https://www.example.com


### Practice 1

1. Configure 2nd vhost `stahuj.<name>.test.local`
2. Add the A record to our [DNS](dns.md) zone
3. Allow listing files for this vhost
4. Create a txt file in document root called `os-info.txt` with same content as /etc/os-release

## Configure HTTPS 
1. Install SSL support

       dnf install mod_ssl
       systemctl restart httpd

2. Generate SSL certificate - self signed

       openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes \
        -keyout /etc/pki/<fqdn>.key -out /etc/pki/<fqdn>.cert -subj "/CN=<fqdn>" \
        -addext "subjectAltName=DNS:<fqdn>,IP:<ip adresa>"

    Show content of certificate in plain text (openssl library):
       
       openssl x509 -in certificate.crt -text -noout

3. Configure virtual host for port 443

       <VirtualHost *:443>
           ServerName www.example.com
           # ... SSL configuration goes here
       </VirtualHost>
    https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html

### Practice 2

1. Create new vhost `secure.<name>.test.local`
2. Serve content from `/var/www/secure.<name>.test.local/web`
3. Generate SSL certificate for domain `secure.<name>.test.local`
4. Add A record to your dns configuration for `secure.<name>.test.local`
5. Serve content: `H1 tag: "Hello, welcome on secure website secure.<name>.test.local."`, use green background
6. Configure vhost to automatically redirect http to https
7. Test via curl `https://secure.<name>.test.local` or via web browser from your laptop