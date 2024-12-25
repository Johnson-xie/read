





TODO

- [ ] 后台框架
- [ ] 接口
  - [ ] create
    - [ ] parse
    - [ ] body
    - [ ] return
  - [ ] update
  - [ ] delete
  - [ ] release
  - [ ] list



## 2024-04-12

- [ ] 账户机器信息

  - [x] CVM
  - [x] domain： juanqilai.club
  - [ ] 证书

- [x] 环境

  - [x] mysql

    ```shell
    yum install mysql
    yum install mysql-devel
    
    wget http://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm
    rpm -ivh mysql80-community-release-el7-5.noarch.rpm
    yum install mysql-community-server
    
    sudo yum install mariadb-server
    rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
    rpm -Uvh https://dev.mysql.com/get/mysql80-community-release-el7-2.noarch.rpm
    yum install mysql-community-server --nogpgcheck
    
    service mysqld restart
    systemctl restart mysqld.service
    
       31  2024-04-12 21:04:18 systemctl start mysqld
       32  2024-04-12 21:04:27 systemctl enable mysqld
       33  2024-04-12 21:04:37 systemctl status mysqld
    
    [root@VM-0-4-centos ~]# grep 'temporary password' /var/log/mysqld.log
    2024-04-12T13:04:20.791646Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: 5&;__sLik;XT
    [root@VM-0-4-centos ~]# mysql -uroot -p
    
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'BG106JfQZiSy%rLSf0#g';
    
    create user 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'BG106JfQZiSy%rLSf0#g';
    
    
    
    
    
    
    
    
    
    
    
    
    '
    ```

  - [x] redis

  - [ ] 

  - [ ] 

    ```shell
       63  2024-04-12 21:29:47 sudo yum install redis
       64  2024-04-12 21:30:02 sudo systemctl start redis
       65  2024-04-12 21:30:11 sudo systemctl enable redis
    ```

  - [ ] golang









### mysql

本地docker launch mysql

```shell
docker pull mysql/mysql-server:8.0

docker run -d --name bike -e MYSQL_ROOT_PASSWORD=qwer1234 -p 3306:3306 mysql/mysql-server:8.0

sudo docker update bike --restart=always


docker exec -it bike bash

mysql -uroot -h127.0.0.1 -p

mysql> CREATE USER 'bike'@'%' IDENTIFIED BY 'qwer1234';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'bike'@'%' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;

mysql -ubike -h127.0.0.1 -p

telnet 127.0.0.1 3306

CREATE DATABASE IF NOT EXISTS bike DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```



```sql
mysql> CREATE USER 'test'@'172.17.0.1' IDENTIFIED BY 'password';
mysql> GRANT ALL ON bike.* TO 'test'@'172.17.0.1';
mysql> flush privileges;
mysql> SELECT user,host FROM mysql.user; 
+------------------+------------+
| user             | host       |
+------------------+------------+
| bike             | %          |
| bike             | 172.17.0.1 |
| test             | 172.17.0.1 |
| healthchecker    | localhost  |
| mysql.infoschema | localhost  |
| mysql.session    | localhost  |
| mysql.sys        | localhost  |
| root             | localhost  |
+------------------+------------+

```





### mongo

```
docker run -d -p 27017:27017 --name test-mongo -e MONGODB_INITDB_ROOT_USERNAME=bike -e MONGODB_INITDB_ROOT_PASSWORD=qwer1234 mongo:latest
```





