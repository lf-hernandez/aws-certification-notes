# AWS Certified Solutions Architect – Associate

## High Level Services Covered On The Exam
- Global Infrastructure
- Compute
- Storage
- Databases
- Network & Content Delivery
- Security, Identity & Compliance

## Table of Contents
- [AWS Global Infrastructure](#aws-global-infrastructure)
- [Identity Access Management (IAM)](#identity-access-management-iam)
  - [What Is It?](#what-is-it)
  - [Features](#features)
  - [Terminology](#terminology)
  - [What can be done from within the Console?](#what-can-be-done-from-within-the-console)


## AWS Global Infrastructure
- Region: Geographical area consisting of 2+ Availability Zones
- Availability Zone: Data Center(s)
- Edge Location: End points used for caching content (Cloud Front)

## Identity Access Management (IAM)

### What Is It?
It's a service that provides a means to manage users and their access level in the AWS Console.

### Features
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

### What can be done from within the Console?
- Assign custom IAM users sign-in link (Account Alias). This is a public URL so it must be unique.
- Activate MFA on root Account.
- Add User(s).
- Use/Create Groups to assign permissions.
- Use/Create Policies to apply to Groups.
- Use/Create Roles to grant permissions to entities.
- Apply IAM password policy.