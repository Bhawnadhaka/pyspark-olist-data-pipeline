# olist-pyspark-data-engineering

A comprehensive data engineering pipeline built with PySpark on Google Cloud Platform's DataProc service, processing and analyzing the Brazilian e-commerce Olist dataset.

## Project Overview

This project implements an end-to-end data processing pipeline for Olist's Brazilian e-commerce dataset, providing valuable business insights through big data techniques. The pipeline consists of four key modules:

1. Data Ingestion and Exploration
2. Data Cleaning and Transformation
3. Data Integration and Aggregation
4. Performance Optimization

## Technologies Used

- **PySpark**: For distributed data processing
- **Google Cloud Platform (GCP)**: Cloud infrastructure
- **DataProc**: Managed Spark service on GCP
- **HDFS**: For data storage
- **Parquet/Snappy**: For efficient data storage format and compression

## Dataset Description

This project utilizes the Olist Brazilian E-commerce dataset, which contains information on orders made at Olist Store. The dataset includes information on 100k orders from 2016 to 2018 across multiple marketplaces in Brazil.

### Database Schema

https://github.com/Bhawnadhaka/pyspark-olist-data-pipeline/blob/main/Screenshot%202025-04-25%20200719.png



## Module 1: Data Ingestion and Exploration

Following a production-grade industry approach to data ingestion:

- Storing the Olist data into HDFS/object storage
- Creating Spark DataFrames for scalable processing


### Key Activities:
t
- Schema validation and metadata analysis
- Initial data quality assessment


## Module 2: Data Cleaning & Transformation

Real-world data engineering practices for cleaning and transforming the Olist dataset:

### Steps in Data Cleaning and Transformation:

1. **Identify Issues**: Handle missing values, duplicate records, and invalid data in Olist tables
2. **Handle Missing Values**: Implement strategies for null values in order and customer data
3. **Standardize Formats**: Convert date/time formats for order and delivery dates, normalize categorical fields
4. **Data Type Correction**: Ensure proper typing for pricing, dates, and IDs across all tables
5. **Deduplication**: Remove duplicate order and product records
6. **Data Transformation**: Apply feature engineering for e-commerce metrics
7. **Store Cleaned Data**: Save processed data in optimized formats (Parquet)

## Module 3: Data Integration & Aggregation

Efficient data integration techniques across the Olist dataset tables:

1. **Join Datasets Efficiently**: Optimize joins between orders, customers, products, and sellers
2. **Optimize Joining Methods**: Select appropriate join strategies for the e-commerce schema
3. **Aggregations**: Implement aggregations for sales metrics, customer behavior, and product performance


## Module 4: Performance Optimization

Techniques to enhance processing efficiency:

- **Data Partitioning**: Optimize Spark jobs by partitioning by order date or geographic region
- **Caching Utilization**: Implement caching for frequently accessed e-commerce metrics
- **Spark Configuration**: Optimize Spark parameters for better performance with the Olist dataset

## Processed Data

The processed dataset is stored in HDFS in Snappy-compressed Parquet format for optimal query performance:

```
root@cluster-0c12-m:/# hadoop fs -ls -h /olist/processed/
Found 11 items
-rw-r--r--   2 root hadoop    0 2025-04-25 11:49 /olist/processed/_SUCCESS
-rw-r--r--   2 root hadoop  8.9 M 2025-04-25 11:49 /olist/processed/part-00000-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  7.7 M 2025-04-25 11:48 /olist/processed/part-00001-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  7.5 M 2025-04-25 11:48 /olist/processed/part-00002-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  9.3 M 2025-04-25 11:49 /olist/processed/part-00003-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  9.1 M 2025-04-25 11:49 /olist/processed/part-00004-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  8.2 M 2025-04-25 11:49 /olist/processed/part-00005-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  9.2 M 2025-04-25 11:49 /olist/processed/part-00006-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  8.3 M 2025-04-25 11:49 /olist/processed/part-00007-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  8.4 M 2025-04-25 11:49 /olist/processed/part-00008-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
-rw-r--r--   2 root hadoop  7.8 M 2025-04-25 11:49 /olist/processed/part-00009-f7a04f7f-63a5-4933-8628-a9908b548edd-c000.snappy.parquet
```



## Business Questions Addressed

This data pipeline enables answering key business questions such as:

1. What are the sales trends over time and by region?
2. Which product categories perform best in terms of revenue and customer satisfaction?
3. How do delivery times affect customer reviews?
4. What are the key factors influencing order cancellations?
5. How do payment methods correlate with order values?



## Getting Started

### Prerequisites

- Google Cloud Platform account
- Installed and configured Google Cloud SDK
- Python 3.7+
- Access to GCP DataProc service

### Setup

#### 1. Clone this repository:
```bash 
git clone https://github.com/Bhawanadhaka/olist-pyspark-data-engineering.git
cd olist-pyspark-data-engineering
```

#### 2. Download the Olist dataset:
The dataset is available from [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)

#### 3. Set up your GCP environment:
```bash
# Set your GCP project
gcloud config set project [MY First Project]

# Create a DataProc cluster
gcloud dataproc clusters create olist-cluster \
    --region=us-central1 \
    --master-machine-type=n1-standard-4 \
    --master-boot-disk-size=50GB \
    --num-workers=2 \
    --worker-machine-type=n1-standard-4 \
    --worker-boot-disk-size=50GB \
    --image-version=2.0-debian10
```

#### 4. Upload data to hdfs:
```pyspark
!hadoop fs -mkdir /olist/processed/
full_orders_df.write.mode('overwrite').parquet('/olist/processed')
hadoop fs -ls -h /olist/processed/
```

### Running the Modules

Each module can be run independently:

```bash
# Run Module 1: Data Ingestion and Exploration
gcloud dataproc jobs submit pyspark module1_ingestion.py \
    --cluster=olist-cluster \
    --region=us-central1 \
    --properties=spark.jars.packages=org.apache.spark:spark-avro_2.12:3.1.2

# Run Module 2: Data Cleaning and Transformation
gcloud dataproc jobs submit pyspark module2_cleaning.py \
    --cluster=olist-cluster \
    --region=us-central1

# Additional modules follow the same pattern
```

### Reading Processed Data

To query the processed data using PySpark:

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder \
    .appName("Olist Data Analysis") \
    .getOrCreate()

# Read processed data
processed_df = spark.read.parquet("hdfs:///olist/processed/")

# Show schema and sample data
processed_df.printSchema()
processed_df.show(5)

# Run analytics queries
# Example: Orders by payment type
payment_summary = processed_df.groupBy("payment_type").count().orderBy("count", ascending=False)
payment_summary.show()
```

## Project Structure

```
olist-pyspark-data-engineering/
├── data/                        # Sample and processed data
├── notebooks/                   # Jupyter notebooks for exploration
├── src/
│   ├── module1_ingestion.py     # Data ingestion and exploration
│   ├── module2_cleaning.py      # Data cleaning and transformation
│   ├── module3_integration.py   # Data integration and aggregation
│   ├── module4_optimization.py  # Performance optimization
│   └── utils/                   # Utility functions
├── config/                      # Configuration files
├── tests/                       # Unit tests
├── results/                     # Analysis outputs and visualizations
├── README.md                    # Project documentation
└── requirements.txt             # Python dependencies
```

## Future Enhancements

- Implement machine learning models for sales forecasting
- Build a real-time dashboard for monitoring key metrics
- Integrate with additional Brazilian market data sources
- Deploy a recommendation engine based on customer purchase patterns
- Add sentiment analysis for customer reviews

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Olist for providing the dataset
- Kaggle platform for hosting the data
- Google Cloud Platform documentation
- Apache Spark and PySpark community
