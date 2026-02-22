# Amazon Aurora – Setup, Connection & Querying

## Overview

In this lab, I worked with Amazon Aurora to set up a managed relational database instance, connect to it via an EC2 instance, and run basic SQL queries against it. This covers the full flow from provisioning to querying.

---

## What I Used

- **Amazon Aurora (MySQL Compatible)** – A fully managed relational database engine that delivers up to five times the performance of standard MySQL, without requiring changes to existing MySQL-based applications.
- **Amazon EC2** – Used as the client machine to connect to the Aurora database via the MySQL client.
- **Amazon RDS** – The service umbrella under which Aurora is managed, handling provisioning, backups, and scaling.

---

## Task 1: Creating the Aurora Instance

I navigated to **RDS** in the AWS Management Console and selected **Create database**, configuring it as follows:

- **Creation method:** Standard create
- **Engine:** Aurora (MySQL Compatible), version 8.0
- **Template:** Dev/Test
- **DB cluster identifier:** `aurora`
- **Master username:** `admin` / **Password:** `admin123`
- **Instance class:** `db.t3.medium` (Burstable)
- **Availability:** No Aurora Replica (not needed for this lab)
- **VPC:** `LabVPC` | **Subnet group:** `dbsubnetgroup` | **Public access:** No
- **Security group:** `DBSecurityGroup` (removed default)
- **Enhanced monitoring:** Disabled
- **Initial database name:** `world`
- **Encryption:** Disabled
- **Auto minor version upgrade:** Disabled

After submitting, the console confirmed:
```
Successfully created database aurora.
```

> Aurora can take up to 5 minutes to provision — I moved on to the next task while it spun up.

---

## Task 2: Connecting to the EC2 Instance

I navigated to **EC2 > Instances** and located the pre-provisioned **Command Host** instance. From there I used **Session Manager** under the Connect options to open a terminal session directly in the browser — no SSH key required.

---

## Task 3: Configuring the EC2 Instance to Connect to Aurora

### Installing the MySQL Client

From the Session Manager terminal, I installed the MariaDB client (which includes the MySQL CLI):
```bash
sudo yum install mariadb -y
```

Expected output confirmed a successful install:
```
Installed:
  mariadb.x86_64 1:5.5.68-1.amzn2.0.1

Complete!
```

### Retrieving the Aurora Endpoint

Back in the RDS console, I opened the `aurora` cluster and went to the **Connectivity & security** tab. I copied the **Writer** endpoint, which looked like:
```
aurora.cluster-cabcdefghijklm.us-west-2.rds.amazonaws.com
```

> Aurora exposes two endpoint types — a **cluster (writer) endpoint** for read/write operations and a **reader endpoint** for load-balanced read-only connections.

### Connecting to Aurora

Using the endpoint I copied, I ran the following command in the terminal:
```bash
mysql -u admin --password='admin123' -h <your-writer-endpoint>
```

A successful connection returned:
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 173
Server version: 8.0.28 Source distribution

MySQL [(none)]>
```

---

## Task 4: Creating a Table, Inserting Data & Querying

### Listing Available Databases
```sql
SHOW DATABASES;
```
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| world              |
+--------------------+
5 rows in set (0.02 sec)
```

### Switching to the World Database
```sql
USE world;
```

### Creating the Country Table
```sql
CREATE TABLE `country` (
  `Code` CHAR(3) NOT NULL DEFAULT '',
  `Name` CHAR(52) NOT NULL DEFAULT '',
  `Continent` enum('Asia','Europe','North America','Africa','Oceania','Antarctica','South America') NOT NULL DEFAULT 'Asia',
  `Region` CHAR(26) NOT NULL DEFAULT '',
  `SurfaceArea` FLOAT(10,2) NOT NULL DEFAULT '0.00',
  `IndepYear` SMALLINT(6) DEFAULT NULL,
  `Population` INT(11) NOT NULL DEFAULT '0',
  `LifeExpectancy` FLOAT(3,1) DEFAULT NULL,
  `GNP` FLOAT(10,2) DEFAULT NULL,
  `GNPOld` FLOAT(10,2) DEFAULT NULL,
  `LocalName` CHAR(45) NOT NULL DEFAULT '',
  `GovernmentForm` CHAR(45) NOT NULL DEFAULT '',
  `Capital` INT(11) DEFAULT NULL,
  `Code2` CHAR(2) NOT NULL DEFAULT '',
  PRIMARY KEY (`Code`)
);
```

### Inserting Records

I inserted five country records into the table:
```sql
INSERT INTO `country` VALUES ('GAB','Gabon','Africa','Central Africa',267668.00,1960,1226000,50.1,5493.00,5279.00,'Le Gabon','Republic',902,'GA');
INSERT INTO `country` VALUES ('IRL','Ireland','Europe','British Islands',70273.00,1921,3775100,76.8,75921.00,73132.00,'Ireland/Éire','Republic',1447,'IE');
INSERT INTO `country` VALUES ('THA','Thailand','Asia','Southeast Asia',513115.00,1350,61399000,68.6,116416.00,153907.00,'Prathet Thai','Constitutional Monarchy',3320,'TH');
INSERT INTO `country` VALUES ('CRI','Costa Rica','North America','Central America',51100.00,1821,4023000,75.8,10226.00,9757.00,'Costa Rica','Republic',584,'CR');
INSERT INTO `country` VALUES ('AUS','Australia','Oceania','Australia and New Zealand',7741220.00,1901,18886000,79.8,351182.00,392911.00,'Australia','Constitutional Monarchy, Federation',135,'AU');
```

### Querying the Data

I ran a filtered query to return countries with a GNP over 35,000 and a population above 10 million:
```sql
SELECT * FROM country WHERE GNP > 35000 AND Population > 10000000;
```

The query returned two results — **Australia** and **Thailand** — both meeting the GNP and population thresholds.

---

## Summary

Through this lab I provisioned an Amazon Aurora MySQL-compatible cluster from scratch, connected to it securely through an EC2 instance using the MySQL CLI, and performed basic DDL and DML operations — creating a table, inserting records, and filtering results with a `SELECT` query. This gave me hands-on exposure to how Aurora fits within the broader AWS RDS ecosystem and how to interact with it programmatically.
