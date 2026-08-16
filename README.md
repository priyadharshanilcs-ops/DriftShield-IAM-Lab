# 🛡️ DriftShield IAM Security Lab

A hands-on AWS cloud security project demonstrating Identity and Access Management (IAM), least-privilege access control, Multi-Factor Authentication (MFA), AWS CloudTrail auditing, and IAM Policy Simulator validation.

## 🎯 Project Objective

The objective of this lab is to demonstrate how AWS IAM can be used to enforce the Principle of Least Privilege and how security controls can be validated through real access attempts, audit evidence, and permission simulation.

## 🏗️ Lab Architecture

```text
Administrator
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
             +-- s3:ListAllMyBuckets --> ALLOWED
             |
             +-- s3:CreateBucket --> DENIED

AWS CloudTrail
     |
     +-- Records authentication and API activity

IAM Policy Simulator
     |
     +-- Validates effective permissions
