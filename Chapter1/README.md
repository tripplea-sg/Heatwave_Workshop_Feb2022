# Create MySQL Database System and HeatWave Cluster
In this lab, you will create and configure a MySQL DB System. You will add a HeatWave Cluster comprise of two or more HeatWave nodes. You will be guided through the following tasks:

    1. Create Virtual Cloud Network
    2. Create MySQL Database for HeatWave (DB System) instance 
    3. Add a HeatWave Cluster to MySQL Database System

## Task 1: Create Virtual Cloud Network
### 1. Click Navigation Menu, Networking, then Virtual Cloud Networks
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn01.png)
### 2. Click Start VCN Wizard
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn02.png)
### 3. Select ‘Create VCN with Internet Connectivity’  
Click ‘Start VCN Wizard’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn03.png)
### 4. Create a VCN with Internet Connectivity 
On Basic Information, complete the following fields: \
VCN Name:
```
MDS-VCN
```
Compartment: Select (root) \
Your screen should look similar to the following
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn04.png)
### 5. Click ‘Next’ at the bottom of the screen 
### 6. Review Oracle Virtual Cloud Network (VCN), Subnets, and Gateways 
Click ‘Create’ to create the VCN 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn04-1.png)
### 7. The Virtual Cloud Network creation is completing 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn05.png)
### 8. Click ‘View Virtual Cloud Network’ to display the created VCN 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn06.png)
### 9. On MDS-VCN page under ‘Subnets in (root) Compartment’, click ‘Private Subnet-MDS-VCN’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn07.png)
### 10. On Private Subnet-MDS-VCN page under ‘Security Lists’, click ‘Security List for Private Subnet-MDS-VCN’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn08.png)
### 11. On Security List for Private Subnet-MDS-VCN page under ‘Ingress Rules’, click ‘Add Ingress Rules’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn09.png)
### 12. On Add Ingress Rules page under Ingress Rule 1 
Add an Ingress Rule with Source CIDR
```
0.0.0.0/0
```
Destination Port Range
```
3306,33060
```
Description
```
MySQL Port Access
```
Click ‘Add Ingress Rule’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn10.png)
### 13. On Security List for Private Subnet-MDS-VCN page, the new Ingress Rules will be shown under the Ingress Rules List 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn11.png)

## Task 2: Create MySQL Database for HeatWave (DB System) instance
### 1. Go to Navigation Menu Databases MySQL DB Systems 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql01.png)
### 2. Click ‘Create MySQL DB System’ 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql02.png)
### 3. Create MySQL DB System dialog complete the fields in each section

    Provide basic information for the DB System
    Setup your required DB System
    Create Administrator credentials
    Configure Networking
    Configure placement
    Configure hardware
    Exclude Backups
    Advanced Options - Data Import

### 4. Provide basic information for the DB System: 
Select Compartment (root) \
Enter Name
```
MDS-HW
```
Enter Description
```
MySQL Database Service HeatWave instance
```
Select HeatWave to specify a HeatWave DB System 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql03-3.png)
### 5. Create Administrator Credentials 
Enter Username (write username to notepad for later use) \
Enter Password (write password to notepad for later use) \
Confirm Password (value should match password for later use) \
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql04.png)
### 6. On Configure networking, keep the default values
Virtual Cloud Network: MDS-VCN \
Subnet: Private Subnet-MDS-VCN (Regional)
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql05.png)
### 7. On Configure hardware, keep default shape as MySQL.HeatWave.VM.Standard.E3 
Data Storage Size (GB) Set value to: 100
```
100
```
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/Heatwave100.png)
### 8. On Configure Backups, disable ‘Enable Automatic Backup’
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql08.png)
### 9. Review Create MySQL DB System Screen 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql09-3.png)
Click the ‘Create’ button \
### 10. The New MySQL DB System will be ready to use after a few minutes 
The state will be shown as ‘Creating’ during the creation 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql10-3.png)
### 11. The state ‘Active’ indicates that the DB System is ready for use 
On MDS-HW Page, check the MySQL Endpoint (Private IP Address) 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/04mysql11-3.png)

## Task 3: Add a HeatWave Cluster to MDS-HW MySQL Database System
### 1. Open the navigation menu
Databases MySQL DB Systems
### 2. Choose the root Compartment. A list of DB Systems is displayed. 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/10addheat01.png)
### 3. In the list of DB Systems, click the MDS-HW system. click More Action -> Add HeatWave Cluster.
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/10addheat02.png)
### 4. On the “Add HeatWave Cluster” dialog, select “MySQL.HeatWave.VM.Standard.E3” shape
### 5. Click “Add HeatWave Cluster” to create the HeatWave cluster 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/10addheat06.png)
### 6. HeatWave creation will take about 10 minutes. From the DB display page scroll down to the Resources section. Click the HeatWave link. Your completed HeatWave Cluster Information section will look like this: 
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/10addheat07.png)
