# ==============================
# SYDNEY TRAFFIC ANALYSIS PROJECT
# Spark + HDFS + Jupyter on Docker
# ==============================

Author: Catherine Varas
Purpose: Run a complete Spark-based Big Data pipeline for Sydney road traffic analytics (2015–2025)
Environment: Google Cloud VM or local Docker host

# Sydney Traffic Analysis – Spark + HDFS on Docker

Containerised big data environment to analyse Sydney road traffic and bus punctuality (2015–2025) using Spark on HDFS, orchestrated with Docker Compose.

## What this project demonstrates

- **Data Engineering on Big Data stacks**
  - Ingestion of multiple CSV datasets into HDFS (`/data/raw`).
  - Schema-aware reads from HDFS via PySpark for analysis and feature creation.

- **Cloud & Containerisation**
  - Reproducible environment with Docker Compose (NameNode, DataNode, Jupyter + Spark).
  - Designed to run on a local host or Google Cloud VM (public IP access to UIs).

- **Practical Spark Engineering**
  - Direct Spark reads from HDFS:
    `spark.read.option("header", True).csv("hdfs://namenode:8020/data/raw/station_ref.csv")`
  - Interactive exploration and transformations in Jupyter notebooks.

## Stack

- Python, PySpark  
- HDFS (NameNode + DataNode)  
- Docker & Docker Compose  
- Jupyter Notebook  
- Linux / Google Cloud VM

-------------------------------------------------------
1. REQUIREMENTS
-------------------------------------------------------
- Docker and Docker Compose installed
- Minimum 8 GB RAM and 20 GB free storage
- Recommended: Ubuntu 22+ or Google Cloud VM (e2-standard-4)

-------------------------------------------------------
2. START THE CONTAINERS
-------------------------------------------------------
Open a terminal in the project folder (where docker-compose.yml is located) and run:

    docker compose up -d

Wait until all three containers are running:
- hdfs-namenode
- hdfs-datanode
- spark-notebook

Check status:
    docker ps

-------------------------------------------------------
3. ACCESS THE SERVICES
-------------------------------------------------------
- Jupyter Notebook:   http://<YOUR_VM_IP>:8888
- NameNode Web UI:    http://<YOUR_VM_IP>:9870
- DataNode Web UI:    http://<YOUR_VM_IP>:9864

No token or password is required.

-------------------------------------------------------
4. VERIFY HDFS IS WORKING
-------------------------------------------------------
Open a terminal:

    docker exec -it hdfs-namenode bash
    hdfs dfs -ls -R /data/raw

Expected output:
    /data/raw/bus_on_time.csv
    /data/raw/road_traffic_counts_hourly_permanent0.csv
    /data/raw/road_traffic_counts_hourly_permanent1.csv
    /data/raw/road_traffic_counts_hourly_permanent2.csv
    /data/raw/road_traffic_counts_hourly_permanent3.csv
    /data/raw/station_ref.csv

If the files are missing, upload them from your local machine:

    hdfs dfs -mkdir -p /data/raw
    hdfs dfs -put /path/to/local/*.csv /data/raw/

Exit the container with:
    exit

-------------------------------------------------------
5. OPEN JUPYTER NOTEBOOK
-------------------------------------------------------
In your browser, open the Jupyter URL and navigate to:
    /home/jovyan/work

Inside that folder, open:
    traffic_analysis.ipynb

If you prefer to upload manually:
- Click “Upload” in Jupyter
- Choose your .ipynb file

-------------------------------------------------------
6. VALIDATE SPARK CONNECTION
-------------------------------------------------------
Inside the first cell of the notebook, run:

```python
spark.read.option("header", True).csv("hdfs://namenode:8020/data/raw/station_ref.csv").show(5)
