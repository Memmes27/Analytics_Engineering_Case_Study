### Load Data into Internal Stages

```sql
USE WAREHOUSE peakdesign_wh;
USE DATABASE peak_design;
USE SCHEMA peak_design.cab;

DESC STAGE peak_design.cab.csv_upload;
list @csv_upload;

COPY INTO peak_design.cab.yellow_taxi
    FROM @peak_design.cab.csv_upload
    file_format = (FORMAT_NAME = peak_design.cab.csv_format)
    on_error = CONTINUE;
    
Remove @csv_upload;
list @csv_upload;
```

![Load_Data](https://github.com/Memmes27/Analytics_Engineering_Case_Study/blob/main/images/Load_Data_Internal_Stages.png)
