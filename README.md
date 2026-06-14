\# 🌐 Azure Hybrid Cloud \& M365 Lab



A comprehensive, production-grade hybrid cloud lab demonstrating the integration of an on-premises enterprise Active Directory infrastructure with Microsoft Entra ID, Microsoft Intune, and Microsoft 365.



\---



\## 🛠️ Technologies \& Skills Demonstrated



!\[Windows Server](https://img.shields.io/badge/Windows%20Server-2022-blue?logo=microsoft)

!\[Azure](https://img.shields.io/badge/Microsoft-Azure-0089D6?logo=microsoft-azure)

!\[Microsoft 365](https://img.shields.io/badge/Microsoft-365-0078D4?logo=microsoft-365)

!\[PowerShell](https://img.shields.io/badge/PowerShell-5391FE?logo=powershell\&logoColor=white)



\* \*\*Directory Services:\*\* Active Directory Domain Services (AD DS), Microsoft Entra ID

\* \*\*Hybrid Identity:\*\* Microsoft Entra Connect, Password Hash Synchronization (PHS)

\* \*\*Modern Management:\*\* Microsoft Intune (MDM/MAM), Hybrid Entra Join

\* \*\*Enterprise SaaS:\*\* Exchange Online, Custom Domain Routing

\* \*\*Virtualization:\*\* Hyper-V (Lab Hosting)



\---



\## 📋 Lab Scope



This lab covers the end-to-end deployment, configuration, and administrative validation of the following hybrid enterprise components:



\* \*\*Identity \& Directory Sync:\*\*

&#x20; \* Alternative UPN Suffix configuration (AD)

&#x20; \* Entra Connect deployment, OU Filtering, and Source Anchor configuration

&#x20; \* User \& Device synchronization

\* \*\*Device Management:\*\*

&#x20; \* Hybrid Microsoft Entra ID Join implementation

&#x20; \* Intune Auto Enrollment \& Enrollment GPO configuration

&#x20; \* Compliance policies enforcement

\* \*\*Cloud Messaging:\*\*

&#x20; \* Custom domain integration (`joeso.au` to Entra ID)

&#x20; \* Exchange Online custom domain mail flow and routing

\* \*\*Administration:\*\*

&#x20; \* PowerShell cmdlet administration, validation, and advanced engineering practices



\---



\## 💻 Lab Environment Architecture



\### 🏢 On-Premises Infrastructure

\* \*\*Domain Controller:\*\* Windows Server 2022

\* \*\*Active Directory Domain:\*\* `joeso.online`

\* \*\*Client Endpoint:\*\* Windows 11 Enterprise (Domain-Joined)

\* \*\*Hypervisor:\*\* Hyper-V Virtual Environment



\### ☁️ Cloud Services (Tenant)

\* Microsoft Entra ID

\* Microsoft Intune

\* Microsoft 365 Business Standard

\* Exchange Online

\* \*\*Verified Custom Domain:\*\* `joeso.au`



\---



\## 🚀 Key Outcomes \& Achievements



\* \*\*Seamless Cloud Sign-In:\*\* Configured Alternative UPN Suffix matching the verified cloud domain for a single-sign-on user experience.

\* \*\*Hybrid Identity Lifecycle:\*\* Successfully synchronized on-premises users and compute devices to Entra ID using Entra Connect.

\* \*\*Modern Endpoint Management:\*\* Implemented Hybrid Microsoft Entra ID Join and automated cloud enrollment into Microsoft Intune via Group Policy (GPO).

\* \*\*Enterprise Mail Flow:\*\* Connected and validated a custom domain with Exchange Online, creating production-ready custom domain mailboxes.

\* \*\*Validation:\*\* Performed deep-dive validation using administrative portals, event logs, and client-side utilities.



\---



\## 🔍 Troubleshooting Covered (Enterprise Support Skills)



> \*\*Note for Recruiters:\*\* A major focus of this lab was simulating, diagnosing, and resolving real-world deployment road-blocks.



\### 🛑 Hybrid Join \& Registration Issues

\* \*\*SCP Validation:\*\* Fixed Service Connection Point (SCP) configuration misalignments in Active Directory.

\* \*\*Device Registration:\*\* Diagnosed registration failures using `dsregcmd /status` analysis and Event Viewer (`User Device Registration` logs).

\* \*\*Identity Duplication:\*\* Resolved duplicate VM identity conflicts in the cloud directory.



\### 🔄 Entra Connect \& Sync Synchronization

\* \*\*OU Filtering Issues:\*\* Corrected synchronization scope problems caused by incorrect OU selection during delta syncs.

\* \*\*Object Hard-Matching:\*\* Validated Source Anchor configurations to ensure seamless user/computer correlation.



\### 📱 Intune Enrollment Roadblocks

\* \*\*MDM User Scope:\*\* Troubleshot enrollment blocks by correctly scoping Entra ID MDM discovery URLs.

\* \*\*Licensing Verification:\*\* Resolved onboarding issues stemming from missing Microsoft 365 / Intune license assignments.

\* \*\*GPO Enforcement:\*\* Traced Group Policy application failures preventing Windows 11 from triggering auto-enrollment.



\### ✉️ Exchange Online Mail Flow

\* \*\*UPN Updates:\*\* Fixed mail routing failures by programmatically updating user Principal Names and primary SMTP addresses.

\* \*\*Autodiscover Testing:\*\* Diagnosed and corrected DNS Autodiscover records to ensure Outlook clients connected without prompt errors.



\---



\## 🔧 Useful PowerShell Commands



The following cmdlets were heavily utilized throughout the provisioning, testing, and lifecycle management phases of the lab:



```powershell

\# Trigger a Delta synchronization to sync changes (Users/OU/Devices)

Start-ADSyncSyncCycle -PolicyType Delta



\# Trigger a Full synchronization cycle

Start-ADSyncSyncCycle -PolicyType Initial



\# Check the current Azure AD Connect synchronization schedule and status

Get-ADSyncScheduler



\# Check local client machine's Hybrid Join and Entra ID status

dsregcmd /status



\# Force immediate Group Policy update on client machines

gpupdate /force

