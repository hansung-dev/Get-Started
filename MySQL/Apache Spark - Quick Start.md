# MySQL 5.7 - Quick Start

## STEP 1: Docker CentOS 환경 구성

```bash
# mysql7 init
docker run -it -p 3306:3306 --name mysql7 --privileged centos:7 init
docker exec -it mysql7 bin/bash
```

```bash
# os init
yum -y update
yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum -y install net-tools
yum -y install wget
```

## STEP 2: Installing MySQL on Linux Using RPM Packages 

```bash
wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
rpm -ivh mysql57-community-release-el7-11.noarch.rpm
yum install mysql-server
```

```bash
systemctl enable mysqld.service
systemctl start mysqld.service
```

## STEP 3: Root Password 변경

```bash
# /var/log/mysqld.log
cat /var/log/mysqld.log | grep root@localhost
# [Note] A temporary password is generated for root@localhost: SiA+iiwD#0cd
```

```bash
mysql_secure_installation
mysql -u root -p
2TF/P!ce*Zqe
```

## STEP 4: User 생성

```bash
# 2TF/P!ce*Zqe
# alter user 'root'@'localhost' identified with mysql_native_password by '2TF/P!ce*Zqe';

create user 'hansung'@'%' identified with mysql_native_password by '2TF/P!ce*Zqe';
GRANT ALL PRIVILEGES ON *.* TO 'hansung'@'%'; 
GRANT GRANT OPTION ON *.* TO 'hansung'@'%'; 
```


## 참조
[Installing MySQL on Linux Using RPM Packages from Oracle](https://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html)
[Basic Steps for MySQL Server Deployment with Docker](https://dev.mysql.com/doc/refman/5.7/en/docker-mysql-getting-started.html)
