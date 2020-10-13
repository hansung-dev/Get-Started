# Apache Airflow - Quick Start

## STEP 1: 환경 구성

```bash
# docker
docker pull jupyter/base-notebook:python-3.7.3

docker run -it -p 8881-8889:8881-8889 -v /Users/hansung.dev/docke jupyter/base-notebook:python-3.7.3 bash
```

```bash
# conda 최신버전으로 업데이트한다
conda update -y conda
# airflow 모듈을 설치한다(버전 1.10.3)
conda install -y airflow
# vim 모듈을 설치한다(소스코드 편집용)
conda install -y vim

pip install werkzeug==0.15.4
```

```bash
airflow initdb
```

```bash
echo ‘export AIRFLOW_HOME=~/airflow’ >> /home/jovyan/.profile
echo ‘export AIRFLOW_HOME=~/airflow’ >> /home/jovyan/.bashrc
source ~/.profile

airflow version
```

## STEP 2: 실습 #1 

```bash
mkdir $AIRFLOW_HOME/dags
```

```bash
cd $AIRFLOW_HOME/dags/ && vim my_first.py

from airflow.models import DAG
from airflow.utils.dates import days_ago
from airflow.operators.bash_operator import BashOperator

args = {‘owner’: ‘jovyan’, ‘start_date’: days_ago(n=1)}
dag  = DAG(dag_id=‘my_first_dag’,
           default_args=args,
           schedule_interval=‘@daily’)

t1 = BashOperator(task_id=‘print_date’,
                  bash_command=‘date’,
                  dag=dag)

t2 = BashOperator(task_id='sleep',
                  bash_command='sleep 3',
                  dag=dag)

t3 = BashOperator(task_id='print_whoami',
                  bash_command='whoami',
                  dag=dag)

t1 >> t2 >> t3
```


```bash
airflow list_dags
airflow list_tasks my_first_dag
airflow test my_first_dag print_date 2019-06-01T09:00:00

airflow scheduler &
airflow webserver -p 8882 &

<http://localhost:8882/admin/>
```

## 참조
* [Apache Airflow Quick Start](https://airflow.apache.org/docs/stable/start.html)
* [Apache Airflow 소개 및 실습하기(기초)](https://m.blog.naver.com/PostView.nhn?blogId=wideeyed&logNo=221565240108&proxyReferer=https:%2F%2Fwww.google.com%2F)
* [Apache Airflow PythonOperator 실습하기(중급)](https://blog.naver.com/wideeyed/221565276777)
