# AWS IAM Security Lab — Users, Groups, Roles & Least-Privilege Policies

## Project Overview
Simulated a real-world AWS Identity and Access Management (IAM) 
setup for a fictional company with three employee types. Created 
users, groups, and roles following the least-privilege principle — 
giving each user only the permissions they need to do their job 
and nothing more.

## Live Architecture
3 Groups → 3 Users → 1 EC2 Role → Permission Testing

## IAM Structure Built

### Groups & Policies
| Group | Policy Attached | What They Can Do |
|-------|----------------|-----------------|
| Admins | AdministratorAccess | Full access to all AWS services including IAM |
| Developers | PowerUserAccess | Full AWS access except IAM and billing |
| ReadOnly | ReadOnlyAccess | View everything, modify nothing |

### Users Created
| Username | Group | Role in Company |
|----------|-------|----------------|
| admin-alvi | Admins | AWS Account Administrator |
| dev-alvi | Developers | Software Developer |
| auditor-alvi | ReadOnly | Security Auditor |

### IAM Role Created
| Role Name | Trusted Entity | Policy | Purpose |
|-----------|---------------|--------|---------|
| EC2-S3-ReadOnly-Role | AWS Service: EC2 | AmazonS3ReadOnlyAccess | Allows EC2 instances to read from S3 without hardcoded credentials |

## Permission Tests & Results

### auditor-alvi (ReadOnly)
| Test | Expected | Result |
|------|----------|--------|
| View S3 bucket contents | ✅ Allowed | ✅ PASSED |
| Delete S3 object | ❌ Denied | ✅ PASSED |
| Create IAM user | ❌ Denied | ✅ PASSED |

### dev-alvi (Developer/PowerUser)
| Test | Expected | Result |
|------|----------|--------|
| Create S3 bucket | ✅ Allowed | ✅ PASSED |
| Create IAM user | ❌ Denied | ✅ PASSED |

## Why Least-Privilege Matters
In a real company, giving everyone AdministratorAccess is a major 
security risk. If a developer's account is compromised, an attacker 
should only be able to access what that developer could — not the 
entire AWS account. This project demonstrates how to implement 
proper access boundaries for different job functions.

## Key Concepts Demonstrated
- IAM Users, Groups, Roles, and Policies
- Least-privilege access control
- AWS managed policies vs custom policies
- Service roles for EC2-to-S3 access
- Permission testing and verification
- Root account security best practices

## AWS Services Used
- AWS IAM (Identity and Access Management)
- Amazon S3 (for permission testing)

## Errors & Findings
- auditor-alvi received Access Denied when attempting to delete 
  S3 objects — confirming ReadOnlyAccess blocks all write operations
- auditor-alvi received "not authorized to perform iam:CreateUser" 
  — confirming ReadOnly cannot modify IAM
- dev-alvi successfully created an S3 bucket — confirming 
  PowerUserAccess grants resource creation rights
- dev-alvi received Access Denied when attempting IAM actions — 
  confirming PowerUserAccess correctly blocks IAM modifications

## Skills Demonstrated
AWS IAM, least-privilege security, user management, group policies, 
service roles, permission testing, cloud security best practices