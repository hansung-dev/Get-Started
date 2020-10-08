# Apache Spark - Quick Start

## STEP 1: 설치

[Docker Hub](https://hub.docker.com/r/rheor108/spark_the_definitive_guide_practice/)
: Spark version: 2.3.2 Python version: 2.7 Zeppelin version: 0.8.0

```bash
docker pull rheor108/spark_the_definitive_guide_practice
docker run -p 8080:8080 -p 4040:4040 rheor108/spark_the_definitive_guide_practice
```
## STEP 2: 접속하기
브라우저에서 접속합니다 - http://localhost:8080 

예제 파일의 노트북을 실행 합니다. (ex. Spark-The-Definitive-Guide-Python)

![spark%2035b1352058f34e63960d18f32a81010b/_2020-10-07__1.00.58.png](spark%2035b1352058f34e63960d18f32a81010b/_2020-10-07__1.00.58.png)

## STEP 3: 간단한 예제 (1)

```bash
%spark.pyspark
myRange = spark.range(1000).toDF("number")
myRange.count()
```
## STEP 4: 간단한 예제 (2)

```bash
%spark.pyspark
divisBy2 = myRange.where("number % 2 = 0")
divisBy2.count()
```

## STEP 4: 조금 간단하지 않은 예제 (1)
#### CSV 읽고 Query로 결과 출력

```bash
%spark.pyspark

flightData2015 = spark\
  .read\
  .option("inferSchema", "true")\
  .option("header", "true")\
  .csv("/data/flight-data/csv/2015-summary.csv")
```

```bash
%spark.pyspark

flightData2015.createOrReplaceTempView("flight_data_2015")

sqlWay = spark.sql("""
SELECT DEST_COUNTRY_NAME, count(1)
FROM flight_data_2015
GROUP BY DEST_COUNTRY_NAME
""")

dataFrameWay = flightData2015\
  .groupBy("DEST_COUNTRY_NAME")\
  .count()

sqlWay.explain()
dataFrameWay.explain()
```

```bash
%spark.pyspark

from pyspark.sql.functions import max
flightData2015.select(max("count")).take(1)
```

## 참조
* [Apache Spark 개요](https://youtu.be/vKee4qOuRmk)
* [Apache Spark 튜토리얼](https://youtu.be/Q8LsnDsy--c)
* [dream2globe/SparkDefinitiveGuide](https://github.com/dream2globe/SparkDefinitiveGuide)
* [FVBros/Spark-The-Definitive-Guide](https://github.com/FVBros/Spark-The-Definitive-Guide/tree/a1f81d09687c227c1401f11d5e7ef1a49651a6f9)
