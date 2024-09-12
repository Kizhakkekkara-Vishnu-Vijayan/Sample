# Database configuration (MySQL, MEMCACHE) 
_**Note: The (#) represents the root directory of the Linux machine and ($) represents all other directories.**_
## 1. MySQL Configuration
### Login to the db vm
>  **$ vagrant ssh db01**
### Verify Hosts entry, if entries missing update the it with IP and hostnames
> **# cat /etc/hosts**
### Update OS with latest patches
> **# yum update -y**
### Set Repository
> **# yum install epel-release -y**
### Install Maria DB Package
> **# yum install git mariadb-server -y**
### Starting & enabling mariadb-server
> **# systemctl start mariadb**
> **# systemctl enable mariadb**
### RUN mysql secure installation script.
> **# mysql_secure_installation**
### [NOTE: Set db root password, I will be using _admin123_ as password]
```
Set root password? [Y/n] Y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
... Success!
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them. This is intended only for testing, and to make the installation
go a bit smoother. You should remove them before moving into a
production environment.
Remove anonymous users? [Y/n] Y
... Success!
Normally, root should only be allowed to connect from 'localhost'. This
ensures that someone cannot guess at the root password from the network.
Disallow root login remotely? [Y/n] n
... skipping.
By default, MariaDB comes with a database named 'test' that anyone can
access. This is also intended only for testing, and should be removed
before moving into a production environment.
Remove test database and access to it? [Y/n] Y
- Dropping test database...
... Success!
- Removing privileges on test database...
... Success!
Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
Reload privilege tables now? [Y/n] Y
... Success!
```
### Set DB name and users.
> **# mysql -u root -padmin123**
```
mysql> create database accounts;
mysql> grant all privileges on accounts.* TO 'admin'@'%' identified by 'admin123';
mysql> FLUSH PRIVILEGES;
mysql> exit;
```
### Download Source code & Initialize Database.
```
git clone https://github.com/Kizhakkekkara-Vishnu-Vijayan/Clone-directory.git
cd vprofile-project
mysql -u root -padmin123 accounts < src/main/resources/db_backup.sql
mysql -u root -padmin123 accounts
```

> mysql> show databases;

![DB_image](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/DB-image.png)

> mysql> show tables;

![DB_image](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Tables.png)


mysql> exit;


### Restart mariadb-server
> **# systemctl restart mariadb**

## 2. MEMCACHE Configuration

### Login to the Memcache vm
> **$ vagrant ssh mc01**
### Verify Hosts entry, if entries missing update the it with IP and hostnames
> **# cat /etc/hosts**
### Update OS with latest patches
> **# yum update -y**
### Install, start & enable memcache on port 11211
```
# sudo dnf install epel-release -y
# sudo dnf install memcached -y
# sudo systemctl start memcached
# sudo systemctl enable memcached
# sudo systemctl status memcached
# sed -i 's/127.0.0.1/0.0.0.0/g' /etc/sysconfig/memcached
# sudo systemctl restart memcached
```

### The sed command is used to search and replace the file content:
#### Before sed command the directory content of /etc/sysconfig/memcached.
![Before-sed](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Before-sed.png)
#### Before sed command the directory content of /etc/sysconfig/memcached.
![After-sed](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/After-sed.png)
#### Replacing the local machine (loop back IP address - 127.0.0.1), with 0.0.0.0, so that remote connection to Memcached service can be established.
