## Data Sources

This project uses publicly available datasets from the **NSW Transport Open Data Portal**.  
The full raw data is **not included in this repository** because the files exceed GitHub’s 100 MB limit (≈3.9 million hourly traffic records).

You must download the datasets manually before running the Spark notebook.

### 1. Road Traffic Counts — Hourly Permanent (4 CSV files)
API-generated hourly traffic volume records for permanent road sensors across NSW.

Download from:  
https://data.nsw.gov.au/data/dataset/2-nsw-roads-traffic-volume-counts-api/resource/d7e887dd-93f1-4417-acb2-0c815a4211af

These files correspond to:

- `road_traffic_counts_hourly_permanent0.csv`  
- `road_traffic_counts_hourly_permanent1.csv`  
- `road_traffic_counts_hourly_permanent2.csv`  
- `road_traffic_counts_hourly_permanent3.csv`  

This dataset contains **3.9+ million hourly observations** across multiple years.

### 2. Road Traffic Counts — Station Reference
Metadata describing each traffic station: road name, region, sensor type, number of lanes, etc.

Download from:  
https://data.nsw.gov.au/data/dataset/2-nsw-roads-traffic-volume-counts-api/resource/f4092c24-87d8-44dc-b23d-83f2ff2a414f

File:

- `road_traffic_counts_station_reference.csv`

---

### Once you have downloaded all files

Move them into:
data/data_sources/

Then **return to the main README** and follow the instructions in: LOAD THE DATA INTO HDFS

That section explains how to copy your local CSV files into the NameNode container and upload them into HDFS before running Spark.
