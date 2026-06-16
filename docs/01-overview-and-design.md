# Overview and Design

## Lab Objective

The objective of this lab is to build a Hybrid Identity environment by integrating an on-premises Active Directory domain with Microsoft Entra ID and Microsoft 365 services.

The lab demonstrates how organizations can synchronize users and devices between on-premises infrastructure and Azure cloud services while maintaining a single identity for authentication and management.

---

## Existing Environment

### On-Premises Environment

- Windows Server 2022 Domain Controller

- Active Directory Domain Services

- Domain Name: **joeso.online**

- Windows 11 Client

- Hyper-V Virtual Environment

### Cloud Environment

- Microsoft Entra ID

- Microsoft 365

- Exchange Online

- Microsoft Intune

---

## Design Challenge

The existing Active Directory domain name is:

```txt
joeso.online
```

The planned public cloud domain is:

```txt
joeso.au
```

Because the on-premises Active Directory environment was already operational, changing the AD domain name was not a practical solution.

Changing an existing Active Directory domain can lead to unnecessary complexity and potential service issues.

---

## Solution

The original Active Directory domain name retained:

```txt
joeso.online
```

An Alternative UPN Suffix added:

```txt
joeso.au
```

This approach allows users to sign in using:

```txt
mike_s@joeso.au
```

while keeping the existing AD structure unchanged.

---

## Hybrid Identity Architecture

The environment was designed using the following architecture:

```txt
On-Prem Active Directory (joeso.online)
        │
        ▼
Microsoft Entra Connect
        │
        ▼
Microsoft Entra ID (Joeso.au)
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
Intune Exchange Microsoft 365
```

---

## Key Components

### Microsoft Entra Connect

Used to synchronize:

- Users

- Groups

- Devices

from Active Directory to Microsoft Entra ID.

### Microsoft Entra ID

Provides cloud identity services and authentication for Microsoft 365 workloads.

### Exchange Online

Provides cloud-based email services using the custom domain:

```txt
joeso.au
```

### Microsoft Intune

Provides cloud-based endpoint management.

---

## Lab Scope

The lab covers:

- public domain registration and DNS Hosting

- AD Alternative UPN Suffix configuration

- Entra ID Custom domain integration

- Microsoft Entra Connect deployment

- Password Hash Synchronization (PHS)

- OU Filtering

- Hybrid Microsoft Entra ID Join

- Device synchronization

- Exchange Online custom domain setup

- Intune Auto Enrollment

- PowerShell administration

- Troubleshooting and validation
