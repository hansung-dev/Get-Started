# PostgreSQL 10.12 - Quick Start

## STEP 1: Docker CentOS7 구축
'''bash
docker run -it -p 6379:6379 —name redis centos:7 bin/bash

yum install epel-release
yum update
yum install -y make wget gcc
'''

## STEP 2: PostgreSQL 설치 (10.12)

```bash
## PostgreSQL Repository 추가하기
rpm -Uvh <https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm>

## PostgreSQL 설치
yum install -y postgresql10-server postgresql10-contrib

## 기본 Database 생성
## data 및 log 경로 변경이 필요하면 profile 에 pgdata 경로 변경 후 실행 필요
/usr/pgsql-10/bin/postgresql-10-setup initdb

## 서비스 실행 및 등록
systemctl start postgresql-10
systemctl enable postgresql-10

# Created symlink from /etc/systemd/system/multi-user.target.wants/postgresql-10.service to /usr/lib/systemd/system/postgresql-10.service.
```

## STEP 3: 환경설정 변경

```bash
## postgres 비밀번호 설정
su - postgres
-bash-4.2$ psql
ALTER USER postgres PASSWORD 'postgres';
\\q

## listen_addresses 설정 변경
vi /var/lib/pgsql/10/data/postgresql.conf
listen_addresses = '*'

## 
vi /var/lib/pgsql/10/data/pg_hba.conf

## dbeaver 다운로드 후 postgres 접근
brew install openjdk
```

## 참조
* [Centos 7에서 PostgreSQL 11 설치하기](https://medium.com/@jinseok.choi/centos-7%EC%97%90%EC%84%9C-postgresql-11-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-77bc0da9d0af)
