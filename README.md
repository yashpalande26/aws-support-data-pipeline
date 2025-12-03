AWS Support Data Pipeline

This project implements an end-to-end ETL pipeline on AWS for ingesting, transforming, and analyzing customer support ticket data and application log data. It demonstrates real-world data engineering practices using Amazon S3, AWS Lambda, AWS Glue, Athena, and Redshift. The pipeline processes structured data (CSV ticket dumps) and semi-structured data (log files), converts them into optimized formats, and makes them available for analytics and BI dashboards.

Project Overview

The pipeline solves the problem of fragmented operational data by consolidating support tickets and application logs into a unified analytics environment. It automates ingestion, transformation, warehousing, and querying.

Data sources:
	•	Support tickets (CSV exported from MySQL)
	•	Application support logs (.log files)

Processed outputs:
	•	Cleaned and standardized Parquet files in S3
	•	Athena external tables for SQL analytics
	•	Redshift tables for BI and dashboarding

Architecture Summary
	1.	Raw data (CSV and log files) is uploaded to Amazon S3.
	2.	AWS Lambda processes log files, extracts fields, cleans data, and writes Parquet output to S3.
	3.	AWS Glue processes ticket CSVs, applies transformations, and stores Parquet output in S3.
	4.	AWS Glue Crawlers register Parquet files as Athena tables.
	5.	Athena is used for SQL analysis directly on S3.
	6.	Data is loaded into Redshift using the COPY command for warehousing and dashboarding.

Technologies Used

AWS Services:
	•	Amazon S3
	•	AWS Lambda
	•	AWS Glue
	•	Amazon Athena
	•	Amazon Redshift
	•	AWS IAM

Other Tools:
	•	Python
	•	Pandas
	•	Boto3
	•	Jupyter Notebooks
	•	Parquet file format

ETL Workflow Details
	1.	Ingestion:
        •	Support ticket CSVs and log files are uploaded manually or programmatically to S3.
        •	S3 serves as the central raw data lake.
	2.	Transformation:
        AWS Lambda (for logs)
        •	Triggered when new .log files are uploaded to S3.
        •	Parses log files with Python and regex.
        •	Converts output to Parquet and stores in S3 processed zone.
        AWS Glue (for support tickets)
        •	Loads CSV files from S3.
        •	Cleans, standardizes schema, handles missing values.
        •	Converts CSV to Parquet and stores in S3 processed zone.
	3.	Analytics Layer:
        Athena:
        •	Glue Crawlers infer schema and create Athena external tables.
        •	SQL analysis on Parquet files directly in S3.
        Redshift:
        •	Data loaded into Redshift using COPY commands.
        •	Optimized for BI dashboards (sort keys, dist keys, encoding).

Example Queries (Athena)

SELECT channel, COUNT(*) FROM support_tickets GROUP BY channel;

SELECT date, COUNT(*) FROM support_logs GROUP BY date ORDER BY date;

Key Features
	•	Automated ETL using AWS Lambda and Glue.
	•	Event-driven processing for log files.
	•	Data Lake with raw and processed zones.
	•	Parquet file format for cost-efficient analytics.
	•	Athena for serverless SQL queries.
	•	Redshift for BI and dashboarding.
	•	Handles structured and semi-structured data.
	•	Demonstrates real-world data engineering patterns.

Skills Demonstrated
	•	AWS data engineering (S3, Lambda, Glue, Athena, Redshift)
	•	ETL pipeline development
	•	Serverless architecture
	•	Data cleaning and transformation using Python
	•	Parquet optimization
	•	SQL analytics
	•	Data warehouse design

Future Enhancements
	•	Add unit tests for log parsing
	•	Add Glue workflows for orchestration
	•	Implement CI/CD using GitHub Actions and Terraform
	•	Add Power BI dashboard export
	•	Implement incremental loading directly into Redshift from Lambda
