# Load HeatWave cluster in MySQL Database System
A HeatWave cluster comprise of a MySQL DB System node and two or more HeatWave nodes. The MySQL DB System node includes a plugin that is responsible for cluster management, loading data into the HeatWave cluster, query scheduling, and returning query result.
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/10addheat00.png)
## Task 1: Load Data to MySQL DB System
### 1. Download airportdb
If not already connected with SSH, connect to Compute instance using Cloud Shell \
(Example: ssh -i ~/.ssh/id_rsa opc@132.145.17….) \
On command Line, download airport DB
```
wget -O airport-db.zip https://bit.ly/3pZ1PiW
```
### 2. Extract airport-db.zip
```
unzip airport-db.zip
```
### 3.On command Line, connect to MySQL using the MySQL Shell client tool with the following command:
```
mysqlsh -uadmin -p -h 10.0.1... --sql
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/heatwave-load-01-shell.png)
