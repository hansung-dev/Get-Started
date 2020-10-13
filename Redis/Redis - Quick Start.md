# Redis - Quick Start

## STEP 1: 환경 구성

```bash
docker run -it -p 6379:6379 —name redis centos:7 bin/bash

yum install epel-release
yum update
yum install -y make wget gcc


wget <http://download.redis.io/releases/redis-5.0.4.tar.gz>
cd redis-5.0.4
cd deps
make hiredis lua jemalloc linenoise 

cd ..
make
make install

cd /usr/local/bin

cd utils/
./install_server.sh

# Port           : 6300
# Config file    : /etc/redis/6300.conf
# Log file       : /var/log/redis_6300.log
# Data dir       : /var/lib/redis/6300
# Executable     : /usr/local/bin/redis-server
# Cli Executable : /usr/local/bin/redis-cli

service redis_6379 {start / stop / restart}
```

## STEP 2: 프로세스 및 로그 확인

```bash
ps -ef | grep redis
redis-cli -p 6379

## 로그 확인
cd /var/log
cat redis_6379.log
```

## 참조
* [Docker Redis 사용하기](https://jistol.github.io/docker/2017/09/01/docker-redis/)
* [Redis - install](https://daddyprogrammer.org/post/1229/redis-single-instance/)
* [Redis 설치 및 실행](https://hyunalee.tistory.com/17)