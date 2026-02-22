# Database Labs

## Overview
Labs I completed exploring AWS database services — both relational and NoSQL options — using the AWS Management Console to create, query, and manage databases in the cloud.

---

## Labs I Completed

| Lab | Description |
|-----|-------------|
| Create an Aurora MySQL Database | Launched an Aurora MySQL instance, connected via EC2, and queried a relational database |
| Create and Query DynamoDB | Created a DynamoDB table, inserted and modified items, and queried data using both Query and Scan operations |

---

## Services I Worked With

- **Amazon Aurora (MySQL Compatible)** — fully managed relational database engine with high performance and availability
- **Amazon RDS** — managed service used to configure and launch the Aurora database instance
- **Amazon DynamoDB** — fully managed NoSQL database with millisecond latency and automatic scaling
- **Amazon EC2** — used as a Command Host to connect to and query the Aurora database via terminal
- **MariaDB Client** — installed on EC2 to establish a MySQL connection to the Aurora endpoint

---

## Key Tasks I Performed

- Configured and launched an Aurora MySQL database instance within a VPC using a dedicated security group and subnet group
- Connected to an EC2 Command Host via Session Manager and installed the MariaDB client
- Retrieved the Aurora cluster endpoint and established a MySQL connection from the EC2 instance
- Created a database table, inserted records, and ran SQL queries to filter results
- Created a DynamoDB table with a partition key and sort key
- Added items with varying attributes to demonstrate NoSQL schema flexibility
- Modified existing items and queried data using both Query and Scan methods
- Deleted a DynamoDB table and all associated data

---

## What I Demonstrated

Through these labs, I demonstrated knowledge of:

- Relational vs NoSQL database models and their appropriate use cases
- Launching and configuring AWS managed database services
- Connecting to and querying a relational database from a remote EC2 instance
- Flexible data modelling in DynamoDB without a fixed schema
- The performance difference between DynamoDB Query and Scan operations
- Database security through VPC configuration and security groups
