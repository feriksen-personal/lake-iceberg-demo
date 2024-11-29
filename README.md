# Overview

Wanted to create an end to end solution for a typical data lake to data warehouse.

We will pick up share prices, ticker reference data etc using polygon.io free API.

# Architecture

TODO: Insert diagram here

Components: 
Name | Description
---|---
S3 | storage
dlt | for ingestion
dbt | for transformations (leveraging datavault4dbt for DWH)
postgres | for DWH and datamart(s).
soda core | for observability
dagster | for orchestration
datahub | for governance/data catalog

# Data Lake (S3 object storage)
Using min.io S3 docker image. 

Bucket name: LAKE_BUCKET

Layout:

Folder L0 | Folder L1 | Folder L2 | Folder L3 | Description
---|---|---|---|---
lz ||| Landing zone
lz | Trading | || Producer/Department/Owner
lz | Trading | polygon || Source System 
bronze |||| Bronze layer. copy of new files found in the lake/landing zone, and created/combined to parquet/iceberg file(s).
silver |||| Silver layer. Iceberg.
gold |||| Gold layer. Ready for consumption 

files will be placed in sub folders (1 folder per day, with [n] files with timestamp appended to the filename.
