# Home Sales Analysis with PySpark

This project demonstrates the use of PySpark for performing various analytical queries on a home sales dataset. The analysis includes calculating average home prices based on specific criteria and comparing query runtimes on cached and uncached data.

## Description

The primary tasks in this project are:
1. Setting up Spark and Java environment.
2. Loading data from an AWS S3 bucket into a Spark DataFrame.
3. Creating temporary views for running SQL queries.
4. Executing a series of analytical queries to derive insights from the home sales data.
5. Caching data to improve query performance and comparing runtimes.
6. Partitioning data and working with Parquet formatted data.

## Requirements

- Spark 3.x
- Java 11
- PySpark
- Findspark
- Pandas

## Setup

1. Install Spark and Java:
    

2. Set environment variables:
    ```python
    import os
    os.environ["JAVA_HOME"] = "C:\Program Files\Java\jdk-22"
    os.environ["SPARK_HOME"] = f"C:\Users\spark-3.5.1-bin-hadoop3"
    ```

3. Initialize a SparkSession:
    ```python
    import findspark
    findspark.init()
    from pyspark.sql import SparkSession
    spark = SparkSession.builder.appName("SparkSQL").getOrCreate()
    ```

## Tasks

1. **Read data from AWS S3:**
    ```python
    from pyspark import SparkFiles
    url = "https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv"
    spark.sparkContext.addFile(url)
    df = spark.read.csv(SparkFiles.get("home_sales_revised.csv"), header=True, inferSchema=True)
    ```

2. **Create a temporary view:**
    ```python
    df.createOrReplaceTempView("home_sales")
    ```

3. **Run analytical queries:**
    - Average price for a four-bedroom house sold per year.
    - Average price of a home for each year the home was built, with 3 bedrooms and 3 bathrooms.
    - Average price of a home with 3 bedrooms, 3 bathrooms, two floors, and >= 2,000 sqft.
    - Average price of a home per "view" rating with avg price >= $350,000.

4. **Cache and validate caching:**
    ```python
    spark.sql("CACHE TABLE home_sales")
    print(spark.catalog.isCached('home_sales'))
    ```

5. **Partition data by "date_built" and read Parquet formatted data:**
    ```python
    df.write.partitionBy("date_built").parquet("home_sales_partitioned")
    df_parquet = spark.read.parquet("home_sales_partitioned")
    df_parquet.createOrReplaceTempView("home_sales_parquet")
    ```

6. **Uncache and validate uncaching:**
    ```python
    spark.sql("UNCACHE TABLE home_sales")
    print(spark.catalog.isCached('home_sales'))
    ```

## References

- [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- [PySpark SQL Module](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql.html)

