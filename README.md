# IT335 Lab 3 – AWS Cloud Security Fundamentals (Capital One Case Study)

## Overview
This lab applies lessons from the 2019 Capital One data breach by configuring foundational AWS security controls across identity, storage, compute, and monitoring. The goal is to understand how proper cloud configuration could have prevented or limited the scope of that breach.

## What Was Configured

### Part 1 – Baseline Screenshots
Captured the initial state of the AWS console, IAM, S3, and EC2 dashboards before making any changes.

### Part 2 – Identity and Access Management (IAM)
- Verified MFA is enabled on the root account
- Created a restricted IAM user: lab-student-user
- Created an IAM group: LabUsers
- Created and attached a least-privilege policy: LabRestrictedPolicy
- Verified the restricted user could not create or modify resources

### Part 3 – Secure S3 Storage
- Created a private S3 bucket: it335-lab3-andre-secure
- Enabled Block all public access across all four settings
- Confirmed permissions in the bucket Permissions tab

### Part 4 – Secure EC2 Instance
- Launched a Free Tier EC2 instance: lab3-secure-instance
- Created a restricted security group: lab3-restricted-sg
- Limited SSH access to my specific IP address only
- Verified IMDSv2 was set to Required to prevent SSRF attacks

### Part 5 – Logging, Monitoring, and Billing
- Reviewed CloudTrail event history showing all API activity
- Checked Billing dashboard to monitor Free Tier usage

### Part 6 – Written Reflection
See lab3-reflection.md

## Connection to Capital One Breach
| Lab Control | Capital One Vulnerability |
|---|---|
| Least Privilege IAM | Overly permissive ISRM-WAF-Role credentials |
| S3 Block Public Access | Unauthorized bulk data exfiltration via S3 sync |
| IMDSv2 + Security Groups | SSRF exploit used to steal temporary credentials |
| CloudTrail Monitoring | 4 month detection gap before breach was discovered |

## Author
Andre Sheppard
Marymount University – IT335
