# ML Engineer Cheat Sheet

## PySpark
### 1. Create session and configuration
```
from pyspark import SparkContext, SparkConf, SQLContext
from pyspark.sql import SparkSession

sparkConf = SparkConf()
sparkConf.setAppName("app_name")

sparkConf.set("spark.executor.instances", "4")
sparkConf.set("spark.executor.cores", "4")
sparkConf.set("spark.executor.memory", "5000m") # 5GB exec memory
sparkConf.set("spark.driver.memory", "5120m") # 5GB driver memory

spark = SparkSession.builder.config(conf=sparkConf).enableHiveSupport().getOrCreate()
```

### 2. Create DataFrame (1)
```
dept = [("Finance",10), 
        ("Marketing",20), 
        ("Sales",30), 
        ("IT",40) 
      ]
deptColumns = ["dept_name","dept_id"]
deptDF = spark.createDataFrame(data=dept, schema = deptColumns)
deptDF.printSchema()
deptDF.show(truncate=False)
```

## Maven
### 1. Create new project (Scala)
```mvn archetype:generate -DarchetypeGroupId=net.alchim31.maven -DarchetypeArtifactId=scala-archetype-simple```
### 2. Build Clean and Test
```mvn clean test```
### 3. Build but Not running tests
```mvn package -DskipTests=true```

