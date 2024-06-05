### Create a Database, Schema, Table

```sql
USE WAREHOUSE peakdesign_wh;
CREATE OR REPLACE DATABASE peak_design;
CREATE OR REPLACE SCHEMA peak_design.cab;

CREATE OR REPLACE transient table peak_design.cab.yellow_taxi(
    VendorID STRING,
    tpep_pickup_datetime TIMESTAMP,
    tpep_dropoff_datetime TIMESTAMP,
    passenger_count INTEGER,
    trip_distance DOUBLE,
    RatecodeID STRING,
    store_and_fwd_flag STRING,
    PULocationID STRING,
    DOLocationID STRING,
    payment_type STRING,
    fare_amount DOUBLE,
    extra DOUBLE,
    mta_tax DOUBLE,
    tip_amount DOUBLE,
    tolls_amount DOUBLE,
    improvement_surcharge DOUBLE,
    total_amount DOUBLE,
    congestion_surcharge DOUBLE,
    airport_fee DOUBLE,
    trip_duration_minutes DOUBLE,
    total_fare DOUBLE
);

USE DATABASE peak_design;
USE SCHEMA peak_design.cab;

-- create a file format 
CREATE OR REPLACE file format peak_design.cab.csv_format
SKIP_HEADER = 1;

DESC file format peak_design.cab.csv_format;
```





