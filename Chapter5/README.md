# Run MySQL Autopilot
MySQL Autopilot provides machine learning automation that improves performance, scalability, and ease of use of HeatWave. It automates the database lifecycle operations including provisioning, data loading, query processing, and error handling. For example:
1. Auto Encoding recommends string column encodings for improving query performance and reducing the amount of memory required on HeatWave nodes.
2. Auto Data Placement recommends data placement keys for optimizing JOIN and GROUP BY query performance. In this lab, you will learn how to use two of the MySQL Autopilot advisors (Auto Encoding and Auto Data Placement) to optimize HeatWave memory usage and performance for your workload

## Task 1: Improve Query performance and Heatwave memory usage using Auto Encoding
### 1. If not already connected with SSH, connect to Compute instance using Cloud Shell
(Example: ssh -i ~/.ssh/id_rsa opc@132.145.170…)
### 2. On command Line, connect to MySQL using the MySQL Shell client tool with the following command:
```
mysqlsh -uadmin -p -h 10.0.1... --sql
```
### 3. Change to the airport database
Enter the following command at the prompt
```
USE airportdb;
```
### 4. If not already on turn on the use_secondary_engine
Enter the following command at the prompt
```
SET SESSION use_secondary_engine=ON;
```
### 5. Run the following four queries and record the runtime:
#### Query 1) Find per-company average age of passengers from Switzerland, Italy and France
```
SELECT
    airline.airlinename,
    AVG(DATEDIFF(departure, birthdate) / 365.25) AS avg_age,
    COUNT(*) AS nb_people
FROM
    booking,
    flight,
    airline,
    passengerdetails
WHERE
    booking.flight_id = flight.flight_id
        AND airline.airline_id = flight.airline_id
        AND booking.passenger_id = passengerdetails.passenger_id
        AND country IN ('SWITZERLAND' , 'FRANCE', 'ITALY')
GROUP BY airline.airlinename
ORDER BY airline.airlinename , avg_age
LIMIT 10;
```
#### Query 2) Find top 10 companies selling the biggest amount of tickets for planes taking off from US airports
```
SELECT
    airline.airlinename,
    SUM(booking.price) AS price_tickets,
    COUNT(*) AS nb_tickets
FROM
    booking,
    flight,
    airline,
    airport_geo
WHERE
    booking.flight_id = flight.flight_id
        AND airline.airline_id = flight.airline_id
        AND flight.from = airport_geo.airport_id
        AND airport_geo.country = 'UNITED STATES'
GROUP BY airline.airlinename
ORDER BY nb_tickets DESC , airline.airlinename
LIMIT 10;
```
#### Query 3) Ticket price greater than 500, grouped by price
```
SELECT
    booking.price, COUNT(*)
FROM
    booking
WHERE
    booking.price > 500
GROUP BY booking.price
ORDER BY booking.price
LIMIT 10;
```
#### Query 4) Ticket price greater than 400, grouped by firstname , lastname
```
SELECT
    firstname,
    lastname,
    COUNT(booking.passenger_id) AS count_bookings
FROM
    passenger,
    booking
WHERE
    booking.passenger_id = passenger.passenger_id
        AND passenger.lastname = 'Aldrin'
        OR (passenger.firstname = 'Neil'
        AND passenger.lastname = 'Armstrong')
        AND booking.price > 400.00
GROUP BY firstname , lastname;
```
### 6. Run Auto Encoding advisor to see if there are any recommendations for string column encodings
```
call sys.heatwave_advisor(json_object('target_schema', JSON_ARRAY('airportdb'), 'auto_enc', json_object('mode', 'recommend') ));
```
### 7. To apply the suggestion, access the auto-generated script
```
SET SESSION group_concat_max_len = 1000000;
```
```
SELECT GROUP_CONCAT(log->>"$.sql" SEPARATOR '\n') AS "SQL Script" FROM sys.heatwave_advisor_report WHERE type = "sql" ORDER BY id;
```
### 8. Copy and paste auto-generated script to apply AutoEncoding changes
### 9. Run the same queries in step 1 and record the time. You can see that total query runtime has improved.
Your results should look like this:
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/pilot01.png)

## Task 2: Improve Query performance using Auto Data Placement
### 1. Run MySQL Autopilot Auto Data Placement advisor to get suggestions on data placement keys.
```
call sys.heatwave_advisor(json_object('target_schema', JSON_ARRAY('airportdb'), 'auto_dp', json_object('benefit_threshold',0) ));
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/pilot02.png)
### 2. To apply the suggestion, access the auto-generated script
```
SET SESSION group_concat_max_len = 1000000;
```
```
SELECT GROUP_CONCAT(log->>"$.sql" SEPARATOR '\n') AS "SQL Script" FROM sys.heatwave_advisor_report WHERE type = "sql" ORDER BY id;
```
### 3. Copy and paste auto-generated script to apply data placement changes
### 4. Run the query in Task 1 step 1 again. You can see that total query runtime has improved.
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/pilot03.png)
