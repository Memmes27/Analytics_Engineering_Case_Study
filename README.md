# Analytics Engineering Case Study
Peak Design Interview - Case Study

# NYC Taxi Data Analysis Case Study

## Overview

This repository contains the analysis of NYC Taxi Trip Data as part of a case study. The objective of the analysis is to understand travel patterns, fare characteristics, and operational insights that could help improve taxi services. The analysis involves data manipulation, analysis, and visualization using Python, SQL, and Looker Studio.

## Case Study Tasks

### 1. Data Acquisition and Cleaning
- **Download the Yellow Taxi trip data for January 2022**: The data was provided as a `.parquet` file.
  https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
  
- **Clean the data by handling missing values, correcting anomalies, and filtering records based on plausible trip distances and fare amounts**:
  - Handled missing values by dropping rows with any missing value.
  - Filtered anomalies based on trip distance (0 < trip_distance ≤ 100) and fare amount (0 < fare_amount ≤ 500).
  - Calculated trip duration in minutes and filtered trips with zero or negative duration or durations longer than 24 hours.
  - Filtered anomalies based on passenger count (0 < passenger_count ≤ 6).
  - Calculated total fare including all surcharges and fees, and filtered out records where total_amount was greater than total_fare.

### 2. Loading Data into Snowflake
- **Export the cleaned data to a CSV file** and upload it to an internal SnowSQL stage for ingestion.
- **Create a Snowflake database, schema, and internal stage** to load the data from the SnowSQL.
- **Create tables in Snowflake** based on the queries needed for analysis.

### 3. Data Analysis Using SQL
- **Calculate the average fare amount and trip distance by time of day**:
  ```sql
  SELECT 
      EXTRACT(HOUR FROM tpep_pickup_datetime) AS pickup_hour,
      AVG(fare_amount) AS avg_fare_amount,
      AVG(trip_distance) AS avg_trip_distance,
      COUNT(*) AS trip_count
  FROM 
      peak_design.cab.yellow_taxi
  GROUP BY 
      EXTRACT(HOUR FROM tpep_pickup_datetime)
  ORDER BY 
      pickup_hour;
  ```

### 4. Visualizing Data in Looker Studio
- **Initital Snowflake - Looker Studio Connector.**
![Snowflake-Looker](https://github.com/Memmes27/Analytics_Engineering_Case_Study/blob/main/images/Snowflake_Looker_Connector.png)
- **Create visualizations in Looker Studio**:
- **Create a new report and add data visualizations based on the tables created in Snowflake.**
- **Visualize average fare amount and trip distance by time of day, peak hours for taxi usage, and the percentage of airport trips.**
  https://lookerstudio.google.com/s/gK7UU2zudtY

### 5. Repository Structure
- **images/: Contains images from the sql src code and the data warehouse.**
- **src/: Contains Python scripts for data cleaning, exporting to CSV, and loading data into Snowflake.**
- **sql/: Contains SQL scripts for datawarehouse setup, creating tables and performing data analysis in Snowflake.**
