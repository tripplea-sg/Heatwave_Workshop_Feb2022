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
mysqlsh -uadmin -p -h 10.0.1... 
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/heatwave-load-01-shell.png)
### 4. Load airport-db into MySQL DB System
```
JS > util.loadDump('airport-db')
```
Switch MySQL Shell mode from JS to SQL
```
JS > \sql
```
Check if airport-db is successfully loaded into MySQL DB System
```
SQL > SELECT table_name, table_rows FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'airportdb';
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/airportdb-list.png)

## Task 2: Load Data to MySQL Heatwave
### 1. Run the following Auto Parallel Load command to load the airportdb tables into HeatWave..
```
SQL > CALL sys.heatwave_load(JSON_ARRAY('airportdb'), NULL);
```
### 2. The completed load cluster screen should look like this:
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/heatwave-load-02.png)
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/heatwave-load-03.png)
### 3. Verify that the tables are loaded in the HeatWave cluster. Loaded tables have an AVAIL_RPDGSTABSTATE load status.
```
SQL > USE performance_schema;
SQL > SELECT NAME, LOAD_STATUS FROM rpd_tables,rpd_table_id WHERE rpd_tables.ID = rpd_table_id.ID;
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/heatwave-load-04.png)



