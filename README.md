# Analytics Engineering Case Study
Peak Design Interview - Case Study

# NYC Taxi Data Analysis Case Study

## Overview

This repository contains the analysis of NYC Taxi Trip Data as part of a case study. The objective of the analysis is to understand travel patterns, fare characteristics, and operational insights that could help improve taxi services. The analysis involves data manipulation, analysis, and visualization using Python, SQL, and Looker Studio.

## Case Study Tasks

### 1. Data Acquisition and Cleaning
- **Download the Yellow Taxi trip data for January 2022**: The data was provided as a `.parquet` file.
  'https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page'
- **Clean the data by handling missing values, correcting anomalies, and filtering records based on plausible trip distances and fare amounts**:
  - Handled missing values by dropping rows with any missing value.
  - Filtered anomalies based on trip distance (0 < trip_distance ≤ 100) and fare amount (0 < fare_amount ≤ 500).
  - Calculated trip duration in minutes and filtered trips with zero or negative duration or durations longer than 24 hours.
  - Filtered anomalies based on passenger count (0 < passenger_count ≤ 6).
  - Calculated total fare including all surcharges and fees, and filtered out records where total_amount was greater than total_fare.

### 2. Loading Data into Snowflake
- **Export the cleaned data to a CSV file** and upload it to an S3 bucket.
- **Create a Snowflake database, schema, and internal stage** to load the data from the SnowSQL.
- **Create tables in Snowflake** based on the queries needed for analysis.

### 3. Data Analysis Using SQL
- **Calculate the average fare amount and trip distance by time of day**:
  ```sql
  CREATE OR REPLACE TABLE my_schema.avg_fare_trip_distance_by_hour AS
  SELECT 
      EXTRACT(HOUR FROM tpep_pickup_datetime) AS pickup_hour,
      AVG(fare_amount) AS avg_fare_amount,
      AVG(trip_distance) AS avg_trip_distance,
      COUNT(*) AS trip_count
  FROM 
      my_schema.taxi_data
  GROUP BY 
      EXTRACT(HOUR FROM tpep_pickup_datetime)
  ORDER BY 
      pickup_hour;

