
# Project 6: AWS RDS – Managed Relational Database

## Project Overview

This project demonstrates how to deploy and connect an Amazon RDS MySQL database to an Amazon EC2 instance.

The objective is to understand how managed relational databases work in AWS and how applications hosted on EC2 can communicate with RDS securely.

This project also demonstrates basic SQL operations, database connectivity, and AWS network security configuration.

## Project Objectives

- Create and configure an Amazon RDS MySQL database.
- Understand managed relational database services.
- Connect an EC2 instance to an RDS database.
- Configure security groups for database connectivity.
- Install and use the MariaDB/MySQL client on Amazon Linux.
- Create database tables and manage records using SQL.
- Test database connectivity and troubleshoot network issues.

## AWS Services and Technologies Used

- Amazon EC2
- Amazon RDS (MySQL)
- Amazon VPC
- AWS Security Groups
- Amazon Linux 2023
- MariaDB/MySQL Client
- SQL

## Architecture Overview

The project uses an EC2 instance as the client machine to connect to an Amazon RDS MySQL database.

**Connection flow:**

1. EC2 instance acts as the database client.
2. MariaDB/MySQL client is installed on EC2.
3. EC2 connects to the RDS database endpoint.
4. Security groups control database connectivity through TCP port 3306.
5. SQL commands are executed to create tables, insert records, and retrieve data.

## Implementation Steps

### 1. Configure Amazon EC2

- Launch an EC2 instance using Amazon Linux 2023.
- Connect to the instance through SSH.
- Verify network connectivity and outbound access.

### 2. Install MariaDB Client

Install the MariaDB client package:

```bash
sudo yum install mariadb105 -y
```

Verify the installation:

```bash
mysql --version
```

### 3. Create Amazon RDS Database

- Create an Amazon RDS MySQL database.
- Configure the database credentials.
- Configure the database networking settings.
- Retrieve the RDS endpoint.

### 4. Configure Security Groups

Configure the RDS security group to allow database connections from the EC2 security group.

| Setting | Configuration |
|---|---|
| Type | MySQL/Aurora |
| Protocol | TCP |
| Port | 3306 |
| Source | EC2 security group |

This allows the EC2 instance to communicate with the RDS database without opening database access to everyone.

### 5. Connect EC2 to Amazon RDS

Use the RDS endpoint to establish a database connection:

```bash
mysql -h YOUR-RDS-ENDPOINT -u YOUR-USERNAME -p
```

Enter the database password when prompted.

### 6. Create Database and Table

Create a database:

```sql
CREATE DATABASE STAFF;
```

Select the database:

```sql
USE STAFF;
```

Create a staff table:

```sql
CREATE TABLE staff (
    id INT,
    name VARCHAR(100),
    phone_number VARCHAR(20)
);
```

### 7. Insert and Retrieve Records

Insert sample records:

```sql
INSERT INTO staff (id, name, phone_number)
VALUES
(1, 'Ali', '0123456789'),
(2, 'Ahmad', '0134567890');
```

Retrieve the records:

```sql
SELECT * FROM staff;
```

View the table structure:

```sql
DESCRIBE staff;
```

## Troubleshooting and Lessons Learned

During this project, I encountered several issues and learned how to troubleshoot them.

**1. Package Installation Failure**

- Encountered Curl error 28 while downloading MariaDB package metadata.
- Investigated EC2 outbound connectivity.
- Adjusted outbound security group access to allow the required network traffic.

**2. SQL Syntax Errors**

- Encountered errors when creating database tables.
- Learned that SQL columns require data types.
- Learned to use commas to separate column definitions.
- Practised correcting incomplete SQL statements.

**3. Database Connectivity**

- Learned how EC2 communicates with Amazon RDS.
- Understood the importance of security group inbound rules and database port 3306.

## Key Skills Gained

- Amazon RDS database deployment and configuration.
- EC2-to-RDS connectivity.
- AWS security group configuration.
- Basic MySQL/MariaDB administration.
- SQL database and table management.
- Network troubleshooting.
- Understanding managed database services.

## Project Outcome

Successfully deployed an Amazon RDS MySQL database and connected to it from an Amazon EC2 instance.

Created a staff table, inserted sample records, and retrieved database information using SQL queries.

This project provided practical experience with managed relational databases and database connectivity within AWS.

## Cost Management

- Stopped or deleted resources when they were no longer required.
- Checked for unnecessary running AWS resources.
- Reviewed storage and networking resources to avoid unexpected charges.

## Conclusion

This project improved my understanding of Amazon RDS, relational databases, and AWS networking.

It also provided hands-on experience connecting compute resources to managed database services using AWS security configurations.
