# Conditional Access and Multi-Factor Authentication

## Overview

Passwords alone are no longer sufficient to protect enterprise identities. Even strong passwords can be compromised through phishing, password reuse or credential leaks.

Microsoft Entra ID addresses this risk by combining **Conditional Access** and **Multi-Factor Authentication (MFA)** to enforce additional identity verification based on organizational security policies.

In this lab, Conditional Access policies were configured to require MFA for Azure Portal access and block legacy authentication. Microsoft Authenticator was used as the primary authentication method, and Microsoft Entra Sign-in Logs were used to validate that the policies were successfully applied.

---

## Lab Objectives

This lab demonstrates how to:

- Configure Authentication Methods in Microsoft Entra ID
- Configure Conditional Access policies
- Require MFA for Azure Portal access
- Block Legacy Authentication
- Register Microsoft Authenticator
- Validate policy enforcement using Sign-in Logs
- Troubleshoot Conditional Access policy evaluation

---

## Authentication Flow

Unlike traditional on-premises Active Directory, Microsoft Entra separates authentication methods from access policies.

The authentication process used in this lab is shown below.

```
User Sign-in
      │
      ▼
Conditional Access Evaluation
      │
      ▼
Require MFA?
      │
      ▼
Authentication Methods
      │
(Microsoft Authenticator)
      │
      ▼
MFA Registration (First Sign-in)
      │
      ▼
Azure Portal Access
```

Conditional Access determines **when** MFA is required, while Authentication Methods determine **which authentication methods users are allowed to register and use**.

---

# Authentication Methods

Authentication Methods are configured independently from Conditional Access policies.

Instead of specifying a particular MFA method inside every Conditional Access policy, Microsoft Entra maintains centralized Authentication Method Policies. When a user is required to perform MFA, Microsoft Entra evaluates which authentication methods are enabled for that user.

For this lab:

- Microsoft Authenticator was enabled for all users.
- SMS authentication remained disabled.
- Microsoft Authenticator was selected as the primary MFA method.

This centralized design allows administrators to modify available authentication methods without editing every Conditional Access policy.

---

# Conditional Access Policy 1 – Require MFA for Azure Portal

The first Conditional Access policy was created to require Multi-Factor Authentication whenever members of the Finance security group access Azure Portal.

**Assignments**

- Users: Finance Security Group
- Target Resource: Azure Management

**Grant Controls**

- Require Multi-Factor Authentication

**Policy State**

- On

This policy protects administrative access to Azure resources by requiring an additional authentication factor after successful password verification.

> *Screenshot: CA001 Policy Configuration*

---

# Conditional Access Policy 2 – Block Legacy Authentication

Legacy authentication protocols such as POP3, IMAP, SMTP AUTH and Exchange ActiveSync do not support modern authentication or MFA.

A second Conditional Access policy was created to block legacy authentication for Exchange Online.

**Assignments**

- Users: Finance Security Group
- Target Resource: Office 365 Exchange Online

**Conditions**

- Client Apps
    - Exchange ActiveSync
    - Other Clients

**Grant Controls**

- Block Access

This prevents users from bypassing MFA through older authentication protocols.

> *Screenshot: CA002 Policy Configuration*

---

# Multi-Factor Authentication Registration

After Conditional Access was enabled, the test user signed in to Azure Portal.

Since no MFA method had previously been registered, Microsoft Entra redirected the user to complete the MFA registration process.

Microsoft Authenticator was installed on a mobile device and linked to the user account by scanning the QR code displayed during registration.

After registration was completed, subsequent sign-ins required approval through Microsoft Authenticator before Azure Portal access was granted.

> *Screenshot: Microsoft Authenticator Registration*

---

# Authentication Methods vs Conditional Access

One important concept learned during this lab is that Authentication Methods and Conditional Access serve different purposes.

| Component              | Purpose                                                  |
| ---------------------- | -------------------------------------------------------- |
| Authentication Methods | Determines which MFA methods a user can register and use |
| Conditional Access     | Determines when MFA is required                          |

For example, Conditional Access simply requires Multi-Factor Authentication. It does not specify whether the user should authenticate with Microsoft Authenticator, SMS or another method.

When MFA is required, Microsoft Entra evaluates the Authentication Method Policies that apply to the user and presents the available authentication methods during MFA registration.

---

# Policy Validation

After completing MFA registration, Azure Portal sign-in was tested again.

Microsoft Entra Sign-in Logs were then reviewed to verify that:

- User authentication succeeded
- Conditional Access policy was evaluated
- CA001 was successfully applied
- MFA requirement was satisfied

The Sign-in Logs provide one of the most valuable troubleshooting tools for administrators because they clearly show which Conditional Access policies were evaluated during each authentication attempt.

> *Screenshot: Sign-in Log showing CA001 applied successfully*

---

# Troubleshooting

## Conditional Access Policy Was Not Applied

### Issue

Although the test user successfully signed in to Azure Portal, the Sign-in Logs did not show that the Conditional Access policy had been applied.

### Investigation

Two configuration issues were identified.

The first issue was that the policy remained in **Report-only** mode instead of **On**. Report-only mode evaluates policies without enforcing them.

After changing the policy state to **On**, the policy still did not apply.

Further investigation showed that the policy targeted a **Microsoft 365 Group** instead of a **Security Group**.

A new Security Group named **Finance** was created, the test user was added to the group, and the Conditional Access policy was updated to target the new Security Group.

After signing in again, Sign-in Logs confirmed that the policy was successfully evaluated and enforced.

### Resolution

- Changed policy state from **Report-only** to **On**
- Replaced the Microsoft 365 Group with a Security Group
- Added the test user to the Security Group
- Verified successful policy evaluation using Sign-in Logs

### Lesson Learned

Always verify both the policy state and the target group assignment when troubleshooting Conditional Access policies. Sign-in Logs provide the most reliable evidence that a policy has been evaluated and applied.

---

## Microsoft Authenticator Registration

### Issue

Before Conditional Access could require MFA, the user had not registered any authentication method.

### Resolution

The user completed Microsoft Authenticator registration by scanning the QR code presented during the first sign-in.

Subsequent sign-ins successfully prompted Microsoft Authenticator for MFA approval.

### Lesson Learned

Authentication Methods define which MFA methods users may register. Conditional Access determines when those registered methods must be used.

---

# Lessons Learned

This lab provided practical experience with Microsoft Entra identity protection and policy-based access control.

Key takeaways include:

- Authentication Methods and Conditional Access are independent components.
- Conditional Access determines when MFA is required.
- Authentication Methods determine which authentication methods users can register and use.
- Microsoft Authenticator provides a more secure MFA experience than SMS-based authentication.
- Sign-in Logs are essential for validating and troubleshooting Conditional Access policy evaluation.
- Report-only mode is useful for testing policies before enforcement.
- Security Groups are recommended when assigning Conditional Access policies in enterprise environments.

---

## Summary

This lab demonstrated how Microsoft Entra Conditional Access and Multi-Factor Authentication work together to secure cloud identities.

By implementing Authentication Methods, Conditional Access policies, Microsoft Authenticator registration and Sign-in Log validation, the lab reproduced a common enterprise identity protection workflow and provided hands-on experience in deploying, validating and troubleshooting policy-based authentication in Microsoft Entra ID.