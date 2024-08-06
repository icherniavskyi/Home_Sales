# Home_Sales

This project analyzes home sales data using Apache Spark. The data is processed to extract insights such as average home prices for different bedroom counts, yearly sales trends, and other metrics using Spark SQL. 

## Installation

To run this notebook, you'll need to have the following installed:

- Apache Spark 3.5.1
- Java JDK 11
- Python 3.x
- Jupyter Notebook

## Alternative to Installation

This script designed to run on Google Colaboratory Services. In order to run the script, please follow these steps by setting up the environment:

1. **Import OS and Proper Spark Version**:
  ```bash
  import os
  spark_version = 'spark-3.5.1'
  os.environ['SPARK_VERSION']=spark_version
  ```

3. **Install Java and Spark**:
    ```bash
    apt-get update
    apt-get install openjdk-11-jdk-headless -qq > /dev/null
    wget -q https://downloads.apache.org/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz
    tar xf spark-3.5.1-bin-hadoop3.tgz
    pip install -q findspark
    ```

4. **Environment Variables**:
    ```python
    import os
    os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-11-openjdk-amd64"
    os.environ["SPARK_HOME"] = "/content/spark-3.5.1-bin-hadoop3"
    ```
5. **Start a SparkSession**:
    ```python
    import findspark
    findspark.init()
    from pyspark.sql import SparkSession
    import time
    spark = SparkSession.builder.appName("SparkSQL").getOrCreate()
    ```

## Data

The dataset used in this analysis is sourced from an AWS S3 bucket:
- [Home Sales Data](https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv)

## Usage

1. **Read the data**:
    Load the CSV data from the specified URL into a Spark DataFrame.

    ```python
    from pyspark import SparkFiles
    url = "https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv"
    spark.sparkContext.addFile(url)
    df = spark.read.csv(SparkFiles.get("home_sales_revised.csv"), sep=",", header=True)
    df.show()
    ```

2. **Create a Temporary View**:
    ```python
    df.createOrReplaceTempView('home_sales')
    ```

3. **Run Queries**:
    Execute Spark SQL queries to analyze the data.

## Analysis

The notebook includes various analyses such as:
- Calculating average home prices based on bedroom count.
- Examining sales trends over the years.
- Identifying the peak selling months.

## Runtime Identification

By using following functions the user can identify the query runtime for differently formated and cached data:

```python
  start_time = time.time()
  print("--- %s seconds ---" % (time.time() - start_time))
```
