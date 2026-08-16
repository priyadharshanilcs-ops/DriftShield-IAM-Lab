# 🛡️ DriftShield IAM Security Lab

A hands-on AWS cloud security lab demonstrating Identity and Access Management (IAM), least-privilege access control, Multi-Factor Authentication (MFA), CloudTrail auditing, and IAM Policy Simulator validation.

## 🎯 Project Objective

The objective of this lab is to demonstrate how AWS IAM can be used to enforce the Principle of Least Privilege and how security controls can be validated through both real-world access attempts and auditing tools.

## 🏗️ Lab Architecture

Admin User
   |
   v
IAM Group: DriftShield-Developers
   |
   v
IAM User: driftshield-dev
   |
   +-- MFA Enabled
   |
   +-- DriftShield-S3-ListOnly Policy
           |
           +-- s3:ListAllMyBuckets → ALLOWED
           |
           +-- s3:CreateBucket → DENIED

AWS CloudTrail
   |
   +-- Records authentication and API activity

IAM Policy Simulator
   |
   +-- Validates effective permissions

## 🔐 Security Controls Implemented

### 1. IAM User and Group

Created an IAM group named:

`DriftShield-Developers`

and added the IAM user:

`driftshield-dev`

Permissions were assigned through the group to demonstrate centralized access management.

### 2. Principle of Least Privilege

A custom S3 policy named:

`DriftShield-S3-ListOnly`

was configured to allow:

`S3:ListAllMyBuckets`

The user was intentionally not granted permission to create S3 buckets.

This demonstrates the Principle of Least Privilege: identities receive only the permissions required for their intended task.

### 3. Multi-Factor Authentication (MFA)

MFA was enabled for the `driftshield-dev` IAM user to strengthen authentication beyond username and password.

This reduces the risk associated with compromised passwords.

### 4. Negative Permission Testing

While signed in as `driftshield-dev`, an attempt was made to create an S3 bucket.

AWS denied the request because the user did not have:

`S3:CreateBucket`

permission.

This demonstrated that the least-privilege policy was being enforced.

### 5. CloudTrail Audit Validation

AWS CloudTrail Event History was used to review activity generated during the lab.

The denied `CreateBucket` attempt was recorded with:

- Event source: `s3.amazonaws.com`
- Event name: `CreateBucket`
- User: `driftshield-dev`
- Result: `AccessDenied`

CloudTrail was also used to inspect console authentication events.

This demonstrates how cloud activity can be traced for security monitoring, investigation, and auditing.

### 6. IAM Policy Simulator Validation

The IAM Policy Simulator was used to validate the effective permissions of `driftshield-dev`.

| AWS Action | Result | Explanation |
|---|---|---|
| `s3:ListAllMyBuckets` | ✅ Allowed | Explicit Allow statement matched |
| `s3:CreateBucket` | ❌ Denied | Implicit deny because no Allow statement matched |

The simulator results confirmed that the IAM policy behaved according to the intended least-privilege design.

## 🧠 Key Security Concepts Demonstrated

- Identity and Access Management (IAM)
- Principle of Least Privilege
- Role of IAM groups
- Identity-based policies
- Explicit Allow
- Implicit Deny
- Multi-Factor Authentication (MFA)
- Authentication vs. authorization
- CloudTrail auditing
- Security event investigation
- Permission validation
- Defense in depth

## 🔎 Key Finding

The lab demonstrated an important AWS authorization principle:

> Access is denied by default unless an applicable policy explicitly allows the requested action.

The user could list S3 buckets because that action was explicitly allowed, while bucket creation remained denied because no matching Allow permission existed.

## 🛠️ AWS Services Used

- AWS Identity and Access Management (IAM)
- Amazon S3
- AWS CloudTrail
- IAM Policy Simulator

## 📸 Evidence

Screenshots in this repository document:

1. IAM user and group configuration
2. Least-privilege S3 policy
3. MFA configuration
4. S3 AccessDenied test
5. CloudTrail audit event
6. IAM Policy Simulator results

> Security note: Sensitive identifiers and authentication information should be redacted from screenshots before publishing.

## 📚 What I Learned

Through this lab, I gained practical experience implementing and validating identity security controls in AWS.

Instead of only configuring permissions, I tested both allowed and denied actions, reviewed the resulting audit evidence in CloudTrail, and independently validated effective permissions using the IAM Policy Simulator.

This reinforced the importance of combining preventive controls, strong authentication, testing, and audit visibility when securing cloud environments.

## 🚀 Future Improvements

Future versions of this project can include:

- IAM roles and temporary credentials
- Permission boundaries
- Resource-based S3 policies
- Conditional access using IAM condition keys
- AWS Organizations Service Control Policies (SCPs)
- CloudTrail alerting and monitoring
- Automated IAM policy deployment using Infrastructure as Code

---

**Project:** DriftShield IAM Security Lab  
**Focus:** AWS Cloud Security | IAM | Least Privilege | MFA | CloudTrail
