# DB server

## Links
- https://www.linuxshelltips.com/install-mariadb-rhel-9/
- https://www.linuxshelltips.com/mysql-database-commands-cheat-sheet-for-linux/
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_using_database_servers/using-mariadb_configuring-and-using-database-servers

## Theory
```
packages: mariadb-server
service: mariadb
ports: 3306/tcp
configs:
    /etc/my.cnf.d/mariadb-server.cnf
    /var/lib/mysql/

Main commands:
    SHOW;
    USE;
    CREATE;
    ALTER;
    DROP;
    SELECT;
```

## Install MariaDB Server in RHEL/CentOS/Rocky

1. Install MariaDB

       dnf install mariadb-server

2. Start and enable MariaDB

       systemctl enable --now mariadb

3. Secure MariaDB installation

       mariadb-secure-installation

4. Login to MariaDB 

       #localy:   mariadb -u <user> -p 
       #remotely: mariadb -h <IP or hostname> -P <port> -u <user> -p 

## Manage DB users

1. Create a user

       CREATE USER lipinond@localhost IDENTIFIED BY "plain_password";
       CREATE USER lipinond@192.168.1.xxx IDENTIFIED BY "plain_password";
       CREATE USER lipinond@ IDENTIFIED BY "plain_password";

2. Create database

       CREATE DATABASE contacts;

3. Grant permission to the databse for user

       GRANT ALL ON contacts.* TO lipinond@localhost;
       GRANT ALL ON contacts.* TO lipinond@192.168.1.xxx;
       GRANT ALL ON contacts.* TO lipinond@;

4. Make the changes valid

       FLUSH PRIVILEGES;

5. Make a changes on current user

       ALTER USER <user> <properties_to_change>;

6. Remove user

       DROP USER '<user>'@'<host>';

7. Show users

       SELECT user,host,plugin from mysql.user;

## Manage Databases

1. List databases

       SHOW DATABASES;

2. Create database

       CREATE DATABASE <db_name>;

3. Use database

       USE DATABASE <db_name>;

4. Remove dtabase

       DROP DATABASE <db_name>;

## Manage tables

1. List tables

       SHOW TABLES;
       DESCRIBE <table_name>;

2. Create table

       CREATE TABLE <table_name> (id INT, title varchar(255), description TEXT, created TIMESTAMP DEFAULT CURRENT_TIMESTAMP);

3. Modify table 

       ALTER TABLE <table_name> ADD COLUMN column_name;

4. Delete table and all it's content

       DROP table <table_name>;

## Manage content

1. Add a row

       INSERT INTO table_name(column_list) VALUES(value_list);
       INSERT INTO table_name(id, title, description, TEXT) VALUES(1,"news", "lorem ipsum lorem ipsum"); 

2. Query content

       SELECT column_name1, column_name2, column_name3 FROM table_name;
       SELECT column_name1, column_name2, column_name3 FROM table_name WHERE condition;

3. Modify row(s)

       UPDATE table_name SET column1=value1;

4. Remove row(s)       

       DELETE from table_name WHERE id=1

## Backup DB

https://www.linuxshelltips.com/mysql-database-commands-cheat-sheet-for-linux/

### Practice 1

1. Create database `tietoevry`
2. Create user `admin`, the user can login from any location
3. User `admin` can manage DB `tietoevry` 
4. Create table `contacts` with 6 columns:
    | column name | parameters |
    | --- | --- |
    | id | int NOT NULL AUTO_INCREMENT PRIMARY KEY |
    | user | varchar(255) NOT NULL |
    | name | varchar(255)
    | email | varchar(128)
    | department | varchar(255)
    | changed | TIMESTAMP DEFAULT CURRENT_TIMESTAMP
5. Insert into table `contacts` following people
    | user | name | email | department |
    | --- | --- | --- | --- | 
    | pepa | Josef Kemr | kemr@tietoevry.cz | UNIX |
    | andrea | Andrea Cerna | cerna@tietoevry.cz | HR |
    | martin | Martin Kadlec | kadlec@tietoevry.cz | WINDOWS |
    | veronika | Veronika Kalocova | kalocova@tietoevry.cz | WINDOWS |
    | marek | Marek Zeleny | zeleny@tietoevry.cz | HR |

### Practice 2
1. Create table `departments` with 4 columns:
    | column name | parameters |
    | --- | --- |
    | id | int NOT NULL AUTO_INCREMENT PRIMARY KEY |
    | name | varchar(255) NOT NULL |
    | description | TEXT
    | changed | TIMESTAMP DEFAULT CURRENT_TIMESTAMP
2. Insert into table `departments` following people
    | name | description |
    | --- | --- | 
    | HR | Human Resources |
    | UNIX | OS Management UNIX |
    | WINDOWS | OS Management WINDOWS |

### Practice 3
1. Prepare a query to show contacts only from department `HR`
2. Change email of user `andrea` to `bila@tietoevry.cz`
3. Delete user `veronika`