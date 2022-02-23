# Run Queries with MySQL Shell
In this lab, you will run queries in HeatWave and in MySQL. You will see the query performance improvements on HeatWave compare to MySQL.
## Task 1: Run Queries in HeatWave
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
### 4. Query 1 - Find per-company average age of passengers from Switzerland, Italy and France
### 5. Before running a query, use EXPLAIN to verify that the query can be offloaded to the HeatWave cluster. You should see “Use secondary engine RAPID” in the explain plan. For example:
```
EXPLAIN SELECT
airline.airlinename,
AVG(datediff(departure,birthdate)/365.25) as avg_age,
count(*) as nb_people
FROM
booking, flight, airline, passengerdetails
WHERE
booking.flight_id=flight.flight_id AND
airline.airline_id=flight.airline_id AND
booking.passenger_id=passengerdetails.passenger_id AND
country IN ("SWITZERLAND", "FRANCE", "ITALY")
GROUP BY
airline.airlinename
ORDER BY
airline.airlinename, avg_age
LIMIT 10\G
```
