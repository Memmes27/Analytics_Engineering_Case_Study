### Data Analysis

#### 1. Calculate the Average Fare Amount and Trip Distance by Time of Day

```sql
  SELECT 
    EXTRACT(HOUR FROM tpep_pickup_datetime) AS pickup_hour,
    ROUND(AVG(fare_amount),2) AS avg_fare_amount,
    ROUND(AVG(trip_distance),2) AS avg_trip_distance,
    COUNT(*) AS trip_count
FROM 
    peak_design.cab.yellow_taxi
GROUP BY 
    EXTRACT(HOUR FROM tpep_pickup_datetime)
ORDER BY 
    pickup_hour;
```

#### 2. Identify Peak Hours for Taxi Usage

```sql
WITH hourly_traffic AS (
    SELECT 
        EXTRACT(HOUR FROM tpep_pickup_datetime) AS pickup_hour,
        COUNT(*) AS trip_count
    FROM 
        peak_design.cab.yellow_taxi
    GROUP BY 
        EXTRACT(HOUR FROM tpep_pickup_datetime)
)
SELECT 
    pickup_hour,
    trip_count
FROM 
    hourly_traffic
ORDER BY 
    trip_count DESC;
```

#### 3. -- Calculate the Percentage of Riders that have Taken a Taxi for (to/from) the Airport
##### -- JFK Airport: 132, LaGuardia Airport: 138, Newark Airport: 1

```sql
SELECT 
    ROUND((SUM(CASE WHEN PULocationID IN (1, 132, 138) OR DOLocationID IN (1, 132, 138) THEN 1 ELSE 0 END) * 100.0 / COUNT(*)),2) AS airport_trip_percentage
FROM 
    peak_design.cab.yellow_taxi;
```
