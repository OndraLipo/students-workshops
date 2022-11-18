# Web server
Install apache, manual
Start/enable
vhosts
secure
```
<VirtualHost *:80>
    ServerName www.example.com
    Redirect / https://www.example.com/
</VirtualHost>

<VirtualHost *:443>
    ServerName www.example.com
    # ... SSL configuration goes here
</VirtualHost>
```
Generate SSL certificate - self signed
```
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes \
  -keyout /etc/pki/evry.test.local.key -out /etc/pki/evry.test.local.cert -subj "/CN=evry.test.local" \
  -addext "subjectAltName=DNS:evry.test.local,IP:192.168.0.193"
```

```
openssl x509 -in certificate.crt -text -noout
```

1. Install apache with ssl support
2. Configure firewall to allow http and https traffic
3. Create vhost <name>.test.local
4. Serve content from /var/www/<name>.test.local/web 
5. Configure vhost to automatically redirect http to https
6. Generate SSL certificate for domain <name>.test.local
7. Add A record to your dns configuration for <name>.test.local
8. Test via curl https://<name>.test.local or via webbrowser