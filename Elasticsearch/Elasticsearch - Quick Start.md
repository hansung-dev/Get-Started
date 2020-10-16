# Elasticsearch - Quick Start

## STEP 1: 환경 구성

```bash
# elasticsearch
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.6.1
# kibana
docker pull docker.elastic.co/kibana/kibana:7.6.1
# logstash
docker pull docker.elastic.co/logstash/logstash:7.6.1
```

## STEP 2: 환경 구성
```bash
vi Dockerfile
FROM elasticsearch:7.3.1

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install —batch analysis-nori

docker build --tag elasticsearch-custom .
```

## STEP 3: 
```bash
# elasticsearch
docker run -p 9200:9200 -p 9300:9300 --name elk-e -e "discovery.type=single-node" elasticsearch-custom

# kibana
docker run -d —link elk-e:elasticsearch-custom --name elk-k -p 5601:5601 docker.elastic.co/kibana/kibana:7.6.1

docker container exec -it elk-k bash
bash-4.2$ vi config/kibana.yml
docker container restart elk-k
```

## STEP 4: 
* 엘라스틱서치 localhost:9200 접속

```bash
curl -XDELETE '<http://localhost:9200/.kibana>'

curl <http://localhost:9200/.kibana>'/_cat/indices?v
```

* http://localhost:9200/
* http://localhost:5601/

## 참조
* [Install Elasticsearch with RPM](https://www.elastic.co/guide/en/elasticsearch/reference/current/rpm.html)
* [[도커 + 엘라스틱서치] Docker로 ElasticSearch ELK 스택 디플로이](https://gem1n1.tistory.com/83)
