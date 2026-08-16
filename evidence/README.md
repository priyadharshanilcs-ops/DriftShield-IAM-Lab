# 🔍 DriftShield IAM Lab — Security Evidence

This folder documents the validation evidence collected during the DriftShield IAM Security Lab.

The objective was to verify that least-privilege IAM permissions work as intended and that AWS security activity can be audited.

## 1. MFA Protection

Multi-Factor Authentication (MFA) was configured for the `driftshield-dev` IAM user.

This adds an additional authentication factor beyond the user's password and strengthens account security.

**Validation:** IAM console showed console access enabled with MFA.

---

## 2. Least-Privilege S3 Access

The `driftshield-dev` user received permissions through the `DriftShield-Developers` IAM group.

The custom policy allows:

`S3 → ListAllMyBuckets`

The policy does not grant permission to create S3 buckets.

This demonstrates the Principle of Least Privilege.

---

## 3. Access Denied Test

The `driftshield-dev` user attempted to create an S3 bucket.

AWS rejected the operation because the user did not have:

`s3:CreateBucket`

This confirms that permissions not explicitly granted by the IAM policy remain denied.

---

## 4. CloudTrail Audit Evidence

AWS CloudTrail recorded the attempted S3 `CreateBucket` operation.

The event showed:

- Event name: `CreateBucket`
- Event source: `s3.amazonaws.com`
- IAM user: `driftshield-dev`
- Error: `AccessDenied`

This demonstrates how CloudTrail provides audit visibility into AWS API activity, including unsuccessful operations.

---

## 5. IAM Policy Simulator Validation

The IAM Policy Simulator was used to validate effective permissions.

| Action | Result | Reason |
|---|---|---|
| `s3:ListAllMyBuckets` | ✅ Allowed | Explicit allow |
| `s3:CreateBucket` | ❌ Denied | Implicit deny — no matching allow statement |

The simulator results confirm that the least-privilege policy behaves as designed.

---

## Security Concepts Demonstrated

- Identity and Access Management (IAM)
- Principle of Least Privilege
- Multi-Factor Authentication (MFA)
- IAM groups and policies
- Explicit Allow
- Implicit Deny
- AWS CloudTrail auditing
- IAM Policy Simulator
- Security validation and evidence collection
