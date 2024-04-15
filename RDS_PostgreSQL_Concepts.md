# AWS RDS PostgreSQL Concepts
---
## High-Availability and Read-replicas
- These are features provided by RDS to enhance the reliability, scalability, and performance of database deployments.
- High Availability in RDS ensures uninterrupted database access during hardware or software failures through Multi-AZ deployments.
- Configuring an RDS database as Multi-AZ automatically creates a standby database in a different Availability Zone. Synchronous replication ensures no delays in data updates, providing redundancy and fault tolerance (*automatic failover from DB --> standby*).
- Read Replicas are additional database instances replicating data from the primary instance, offloading read-heavy workloads to enhance DB performance and scalability. Asynchronous replication between DB  & read replicas (*slight delays in data updates*). These replicas can be provisioned in the same AZ (*free*), Multi AZ (*free*) or Cross region (*cost incurred*).

## Snapshotting
- This refers to the process of creating backups of your database instances in a point-in-time manner (*copy of data stored in a database at a specific point in time*).
- It captures the entire state of your database at the moment the snapshot is taken including the data, schema, configuration, and transaction logs.
- Snapshotting serves serval purposes such as:
  - Data Protection (*prevent accidental deletions*)
  - Migration & Diaster Recovery (*migrate database between AWS regions and accounts*)
  - Database Cloning & Testing
  - Point-In-Time-Recovery 

## Backup and recovery
- This is the process of protecting your database's data and configurations and restoring them to a prior state in the event of data loss, corruption, or other issues.
- RDS provides two types of backups: 
  - **Automated backups** (*Enabled by default*): Automatically backup of database daily, with a specified rentention period.
  - **Manual snapshots**: User manually creates snapshots that are store indefinetly until explictly deleted.
- Automated backups enables users to restore RDS database to a specific point in time within the retention period, alternatively can restore database from a manual snapshot to any compatible instance.

## Maintenance window
- This refers to a designated time frame in which AWS performs maintenance tasks, updates, and patches on your RDS instance.
- RDS provides various approachs to managing maintenance activities including, **Scheduled Maintainance**, **User-defined Maintainace Window**, **Notifications**, and **Automatic Maintainance**.

## Authentication and Authorisation options
- In AWS RDS there are several authentication and authorization options available to control access to your database instances and manage user permissions effectively.
- **Database Authentication**: 
  - Database credentials - Can authenticate users via username & password provided by the database engine (e.g., MySQL, PostgreSQL, SQL Server).
  - IAM Database Authentication - Can authenticate users directly through AWS IAM. IAM users or roles can be mapped to database users, offering a secure and centralized approach to managing database access.
- **Database Authorisation**: 
  - IAM Roles and Permissions - Can establish roles with specific permissions and assign them to users.
  - Fine-Grained Access Control - This mechanism enables restricting access to sensitive data based on user attributes or conditions.

## Encryption configuration
- AWS RDS provides several encryption configurations available to enhance the security of your database instances and protect data both at rest and in transit. 
- **Encryption at Rest**: 
  - AWS Managed Key (AWS KMS) - RDS supports encryption at rest with AWS KMS, offering the option to use either AWS-managed keys or customer-managed keys (CMKs).
- **Encryption in Transit**: 
  - SSL/TLS Encryption - RDS supports SSL/TLS encryption for database connections, securing data transmission between your application and the database to prevent interception or eavesdropping.

## Upgrading the database engine
- This refers to the process of migrating an existing database instance to a newer version of the database engine software.
- The process of upgrading an RDS database engine involves:
  - Compatibilty checks (*ensure existing database is compatible with target*),
  - Database Backup (*ensure a snapshot of database exists before initiating the upgrade process*), 
  - Engine upgrade (*ensure desired engine version is selected via RDS console/CLI*),
  - Post-Upgrade testing (*ensure correct functionality of new database*)
  - Monitoring & Optimization (*ensure optimal performance & stability of new database*)

## Secure connection to database using SSL/TLS
- This refers to an encrypted connection between the client application and the database instance to ensure data confidentiality and integrity.
- SSL/TLS encryption is enabled on RDS instance through the RDS console, or AWS CLI (*ensures database instance is configured to accept encrypted connections*). 
- Client application code or configuration must specify SSL/TLS encryption to be used when connecting to the database.
- The client application verifies the SSL/TLS certificate presented by the RDS instance to ensure it is valid and issued by a trusted certificate authority (*ensures the authenticity of the server*).

## Importing data into a database instance
- Importing data into an RDS database instance can be achieved using various methods such as:
  - Native Database Tools/Commands (*pg_dump*) to import data from dump files or data files.
  - AWS DMS to perform a full load or CDC (*continous replication*).
  - AWS Data Pipeline to create tasks for importing data into RDS instances from various sources using templates or custom configurations.
  - Third-party tools and utilities available for importing data into databases, including pgloader for PostgreSQL.

## Invoking an AWS Lambda function from RDS for a PostgreSQL DB instance
- Can invoke a lambda function via AWS Lambda's integration with Amazon RDS.
- Steps include:
  - **Creating an AWS Lambda Function** - Write code using the AWS Lambda console, SDK, or CLI. Configure the Lambda function to handle events triggered from the RDS instance.
  - **Configuring IAM Permissions** - Assign appropriate IAM permissions to Lambda function to allow it to access other AWS resources, including RDS.
  - **Enabling AWS Lambda Integration in RDS** - This is done through the RDS console, where you configure event source settings like the Lambda function to invoke and the triggering database events.
  - **Testing and Monitoring** - Test the invocation by performing database operations on your RDS instance and monitor CloudWatch logs to ensure the Lambda function responds as expected.