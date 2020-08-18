# AWS Certified Solutions Architect – Associate

## High Level Services Covered On The Exam

- Global Infrastructure
- Compute
- Storage
- Databases
- Network & Content Delivery
- Security, Identity & Compliance

## Table of Contents

- [AWS Certified Solutions Architect – Associate](#aws-certified-solutions-architect--associate)
  - [High Level Services Covered On The Exam](#high-level-services-covered-on-the-exam)
  - [Table of Contents](#table-of-contents)
  - [AWS Global Infrastructure](#aws-global-infrastructure)
  - [Identity Access Management (IAM)](#identity-access-management-iam)
    - [IAM - What is it](#iam---what-is-it)
    - [IAM - Features](#iam---features)
    - [Terminology](#terminology)
    - [What can be done from within the Console](#what-can-be-done-from-within-the-console)
  - [Simple Storage Service (S3)](#simple-storage-service-s3)
    - [S3 - What is it](#s3---what-is-it)
    - [S3 - Features](#s3---features)
    - [Object structure](#object-structure)
    - [Consistency model](#consistency-model)
    - [Guarantees](#guarantees)
    - [Tiers [sorted by price]](#tiers-sorted-by-price)
    - [How are you billed](#how-are-you-billed)
    - [Transfer acceleration](#transfer-acceleration)
    - [Cross region replication](#cross-region-replication)
    - [Scenarios for each Tier](#scenarios-for-each-tier)
    - [Security & Encryption](#security--encryption)

## AWS Global Infrastructure

- Region: Geographical area consisting of 2+ Availability Zones
- Availability Zone: Data Center(s)
- Edge Location: End points used for caching content (Cloud Front)

## Identity Access Management (IAM)

### IAM - What is it

It's a service that provides a means to manage users and their access level in the AWS Console.

### IAM - Features

- Centralized control
- Shared access
- Granular Permissions
- Identity Federation
- Multi-factor Authentication
- Temporary access for users, devices, services
- Password rotation policy
- AWS services integration
- PCI DSS Compliance (Credit Card)

### Terminology

- Users: people, employees, etc.
- Groups: collection of users. Permissions are inherited for each user.
- Policies: JSON documents describing what permissions are attributed to a User, Group, and/or Role.
- Roles: Assignable permissions given to AWS Resources to interact with other AWS Resources
- Root Account: Account used to register for AWS. Essentially has Super User access and should be avoided. Defer most tasks to user accounts.

### What can be done from within the Console

- Assign custom IAM users sign-in link (Account Alias). This is a public URL so it must be unique.
- Activate MFA on root Account.
- Add User(s).
- Use/Create Groups to assign permissions.
- Use/Create Policies to apply to Groups.
- Use/Create Roles to grant permissions to entities.
- Apply IAM password policy.

## Simple Storage Service (S3)

### S3 - What is it

Object-based cloud storage.

### S3 - Features

- Object-based (key-value pair)
- File size can range from 0 Bytes to 5 TB
- Unlimited storage
- Objects are stored in Buckets
- Bucket names are universal namespaces, they must be unique globally
- Versioning
- Tiered Storage
- Lifecycle Management
- Encryption
- MFA on Delete
- Securing via Access Control Lists & Bucket Policies
- HTTP status codes are used to describe operation state e.g. HTTP 200 on successful upload

### Object structure

- Key
- Value
- Version ID
- Metadata
- Sub-resources
  - Access Control Lists
  - Torrents

### Consistency model

- Read after write consistency for PUTS of new objects
- Eventual consistency for overwrite PUTS and DELETES

### Guarantees

- 99.99% availability
- 99.999999999% durability for S3 information (Eleven Nines)

### Tiers [sorted by price]

- S3 Standard
  - Guarantees listed above
  - Redundant storage across multiples devices in multiple facilities
  - Designed to sustain loss of two facilities concurrently
- S3 - IA (Infrequently Accessed)
  - For infrequently accessed data that requires rapid access when needed
  - Lower Fee than S3 Standard
  - Charges retrieval fee
- S3 - Intelligent Tiering
  - AI-based option that optimizes cost byt automatically moving data to the most effective access ties based on usage
- S3 One Zone - IA
  - Lower-option for infrequently accessed data
  - For files that don't require multiple AZ data resilience
- S3 Glacier
  - Designed for data archiving
  - Reliable storage at costs competitive with or cheaper than on-premise solutions
  - Retrieval time configurable from minutes to hours
- S3 Glacier Deep Archive
  - Lowest-cost storage class
  - Acceptable retrieval time of up 12 hours or more

### How are you billed

- Storage
- Requests
- Storage management pricing (Tiers)
- Data transfer pricing
- Transfer acceleration
- Cross region replication pricing
  
### Transfer acceleration

Takes advantage of Cloud Front Edge Locations to optimize data transfer network paths over long distances between the S3 bucket and it's end users. End user -> EL -> S3 vs End user -> S3

### Cross region replication

Replication of objects across different buckets in different regions. Use case: high availability and disaster recovery

### Scenarios for each Tier

Almost always go with Intelligent Tiering, it tends to be cheaper and makes use of both Standard and IA. If you need something lower-cost without redundancy go with One Zone IA, but understand that if the AZ fails you could loose your data. For archiving go with Glacier if data is accessed more than once or twice a year, otherwise go with Glacier Deep Archive

### Security & Encryption

By default, newly created buckets are private.

You can setup Access Control on buckets using:

- Bucket Policies
- Access Control Lists

Logging can be configured and will generate access logs for all requests made to the bucket for which it's configured. You can then send those logs to another bucket on the same account or another bucket in another account.

Types of encryption:

- **Encryption In Transit**
  - SSL/TLS
- **Encryption At Rest**
  - Server Side Encryption
    - S3 Managed Keys (SSE-S3)
      - S3 Managed AES-256 Encryption
    - AWS Key Management Service Managed Keys (SSE-KMS)
      - Shared Management
    - SSE with Customer Provided Keys (SSE-C)
      - Customer Managed
  - Client Side Encryption
    - Encrypt object locally before uploading to S3
