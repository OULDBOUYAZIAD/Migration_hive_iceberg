# Migration from Hadoop Architecture to Modernized Architecture with Iceberg


### Introduction :

This repository contains a step-by-step guide for migrating from a traditional Hadoop architecture to a modernized architecture using Apache Iceberg. The migration process involves three main steps:


<p align="center">
    <img src="img/archi.png" alt="Logo" width="600" height="700" >
</p>

1.  Transferring files from HDFS to S3.
2.  Converting Hive tables to Iceberg tables.
3.  Migrating the catalog from Hive Metastore to Nessie.


By following this guide, you will be able to leverage the benefits of Iceberg,



## Table of Contents

- [Introduction](#Introduction)
- [Prerequisites](#Prerequisites)
- [Transferring_Files_from_HDFS_to_S3](#Transferring_Files_from_HDFS_to_S3)
- [Converting_Hive_Tables_to_Iceberg_Tables](#Converting_Hive_Tables_to_Iceberg_Tables)
- [Migrating_the_Catalog_from_Hive_Metastore_to_Nessie](#Migrating_the_Catalog_from_Hive_Metastore_to_Nessie)
- [Conclusion](#Conclusion)

## Prerequisites 

- Hadoop cluster with hive tables and files parquet/orc of this table in the hdfs 
- Minio instance
- Notebook spark 
- Nessie instance

## Step 1: Transferring_Files_from_HDFS_to_S3

1. Copy files from HDFS to S3: 
    
   Copy the parquet/orc file of your table from hdfs to the target bucket using this command :

``` sh
   hadoop distcp hdfs://namenode:8020/path/to/hdfs/directory s3a://your-bucket/path/
```

2. Update Hive table location:

Once the files are copied to S3, update the location of your Hive tables to point to the new S3 location. Connect to your Hive metastore and run the following command:

``` sh
   ALTER TABLE your_table SET LOCATION 's3a://your-bucket/path/';
```

## Step 2: Converting_Hive_Tables_to_Iceberg_Tables


