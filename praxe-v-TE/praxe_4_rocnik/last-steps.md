# Final test

1. Create folder /management owned by petr:management, user `petr` can write/read/execute. User `Anna` can only read. (Create users and give them some passwords.)

2. Deny SSH access for user `root`

3. On disk vdb create physical volume and volume group: `data`. In this volume group create logical volume: `foto` with size 500MB, create ext4 filesystem and mount it persistently to /foto.

4. Extend logical volume `foto` to 650MB

5. Export folder `/foto` as NFS share in read, write mode. Mount it to your ~~workstation~~ server.

6. Create a samba share folder `/filmy` and mount it on your ~~workstation~~ server. Accessible for anyone.

~~7. Create DNS server and forward zone `ostrava.com`~~

~~8. Add following records to zone `ostrava.com`~~
    ```
    dns IN  A   192.168.0.X 
    www IN  A   192.168.0.X
    ```
    (where X is IP of your machine)

9. Install apache

10. Create new vhost `www.ostrava.com`

11. Serve content from `/var/www/www.ostrava.com`

12. Serve content: `H1 tag: "Hello, welcome on secure website www.ostrava.com."`, use yellow background

~~13. Install maridadb~~

~~14. Create database `frydek`~~

~~15. Create user `master`, the user can login from any location~~

~~16. User `master` can manage DB `frydek` ~~

~~17. Create table `uciele` with 6 columns:~~
    | column name | parameters |
    | --- | --- |
    | id | int NOT NULL AUTO_INCREMENT PRIMARY KEY |
    | user | varchar(255) NOT NULL |
    | name | varchar(255)
    | email | varchar(128)
    | class | varchar(255)
    | changed | TIMESTAMP DEFAULT CURRENT_TIMESTAMP

18. Create a shell script that gets 2 numbers from stdin and print *,+,-,/. (optional)