# 💼 ADF Metadata-Driven Pipeline

The purpose of this repository is to demonstrate how to build scalable, maintainable, and reusable data pipelines in Azure Data Factory (ADF) — a cloud-native ETL/ELT tool in the Microsoft Azure ecosystem.

This solution uses a metadata-driven architecture, allowing pipelines to dynamically ingest and process data from various source types such as:

ODBC sources (e.g., legacy SQL systems)

SMB shares (e.g., flat files like .csv or pipe-delimited .txt)

REST APIs (e.g., external data providers or SaaS apps)

## 🧠 Key Features

Control Table-Driven Logic: Ingestion rules and configuration are centrally defined via a metadata table (e.g., md_Source) that drives pipeline execution.

Dynamic Datasets & Linked Services: Supports parameterized datasets and linked services for various source types.

Delta & Full Loads: Supports both Delta loads using watermark columns and Full reloads.

Flexible File Formats: Handles output in formats like parquet, csv, etc.

Dynamic Pathing & Naming: Output paths and filenames are generated on-the-fly using metadata, UTC timestamps, etc.

Parameter Splitting: QueryOrParams values like delimiter=|;header=true are parsed to extract necessary parameters for flexible ingestion.

## 🧪 Technologies Used

* Azure Data Factory v2

* Azure Data Lake Storage Gen2

* Azure SQL Database (for metadata)

* ODBC, REST, SMB integration

* Parquet, CSV file formats

## 🔧 How to Use

1. Deploy Metadata Table: Use the provided schema to deploy your md_Source table.

2. Configure Sources: Populate the metadata table with the source system details (ODBC, REST, SMB).

3. Set up ADF Pipelines: Import pipelines from this repo into ADF.

4. Run Master Pipeline: Triggers ingestion for all active sources dynamically.

## 🧩 Sample Metadata Row (for SMB)
```json
{
  "SourceId": 2,
  "SourceType": "SMB",
  "SourceName": "Payroll_Timesheets",
  "LinkedService": "LS_LEGACY_SMB",
  "ObjectOrPath": "\\\\BaapDataSet\\\\payroll\\\\in\\\\Timesheets_*.txt",
  "QueryOrParams": "delimiter=|;header=true",
  "LoadType": "PerFile",
  "WatermarkCol": null,
  "TargetPath": "adls:/bronze/payroll/timesheets/",
  "FileFormat": "parquet",
  "Active": true
}
```

## 👨‍💻 Author

> Built with 💪 by Mihir Bhadauria
> Connect with me on [LinkedIn](https://www.linkedin.com/in/mihir-bhadauria/)
