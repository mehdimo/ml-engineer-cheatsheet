# ML Engineer Cheat Sheet

## Python
### 1. Virtual Environment
```
python -m venv ./venv
. ./venv/bin/activate
```
* Run `deactivate` in the command line to deactivate the virtual env.

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
### 3. Create DataFrame (2)
```
#define schema
from pyspark.sql.types import StructType,StructField, StringType, IntegerType, DoubleType
schema = StructType([ \
    StructField("id", IntegerType(), True), \
    StructField("name",StringType(),True), \
    StructField("grade", DoubleType(), True) \
  ])
data2 = [(100, "James", 80.0),
    (101, "Michael", 75.5),
    (102, "Robert", 90.2)
  ]
df = spark.createDataFrame(data=data2, schema=schema)
```

## Maven
### 1. Create new project (Scala)
```mvn archetype:generate -DarchetypeGroupId=net.alchim31.maven -DarchetypeArtifactId=scala-archetype-simple```
### 2. Build Clean and Test
```mvn clean test```
### 3. Build but Not running tests
```mvn package -DskipTests=true```

## Docker

### Build docker image from a Dockerfile
  - Change directory to the folder where `Dockerfile` resides.
  - Run `docker build -t {your_image_name} .`
    - `-t` tags your image as a human-readable name for the final image.
    - The `.` at the end tells docker to look for Dockerfile inside the current folder.

### Run docker container from image name
 - `docker run --name {countainer_name} -p 8081:8081 {your_image_name}`
   - `--name` assigns a name to the container. If not specified, a random name would be set.
   - `-p` creates a port mapping between the host and the container.

### Run docker with volume mount given the image Id
```
# by docker image Id
docker run \
-p 8080:8080  \
-v /local/path/:/path/in/docker/ \
bf3c64c34b80  \
serve
```
 - `-v` maps local file/folder to a file/folder in container. 

## Documentation Tools

### Convert .MOV/.MP4 video to .GIF
* Install `ffmpeg` and `gifsicle` if not installed yet.
```
$brew install ffmpeg
$brew install gifsicle
```
* Convert your file to gif:
```
$ffmpeg -i in.mov -pix_fmt rgb8 -r 10 output.gif && gifsicle -O3 output.gif -o output.gif
```
* Arguments:
  - input path argument `-i`
  - pixel format argument `-pix_fmt`
  - removing some frames using framerate argument `-r`
  - end `ffmpeg` with new path/to/filename
