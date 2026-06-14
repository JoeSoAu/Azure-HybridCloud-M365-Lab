\# Azure Hybrid Cloud M365 Lab



This lab demonstrates the setup of an Hybrid-cloud of an On-prem Active Directory integrating with on-premises Microsoft Azur Entra ID and Microsoft 365.



\## Technologies



\- Windows Server 2022

\- Active Directory Domain Services

\- Microsoft Entra ID

\- Microsoft Entra Connect

\- Microsoft Intune

\- Exchange Online

\- Hyper-V

\- PowerShell



\## Lab Scope



\- Alternative UPN Suffix configuration (AD)

\- Custom domain integration (Entra ID)

\- Exchange Online custom domain mail flow

\- Entra Connect deployment

\- Password Hash Synchronization

\- OU Filtering

\- Source Anchor configuration

\- Hybrid Microsoft Entra ID Join

\- Intune Auto Enrollment

\- Device synchronization

\- Compliance policies

\- PowerShell cmdlet administration

\- Troubleshooting and validation



\## Lab Environment



\### On-Premises



\- Windows Server 2022 Domain Controller

\- Active Directory Domain: joeso.online

\- Windows 11 Client

\- Hyper-V Virtual Environment



\### Cloud Services



\- Microsoft Entra ID

\- Microsoft Intune

\- Microsoft 365 Business Standard

\- Exchange Online

\- Custom Domain: joeso.au



\## Key Outcomes



\- Configured Alternative UPN Suffix for cloud sign-in

\- Synchronized on-premises users and devices to Entra ID

\- Implemented Hybrid Microsoft Entra ID Join

\- Configured Microsoft Intune Auto Enrollment

\- Connected a custom domain to Microsoft 365

\- Configured Exchange Online custom domain mailboxes

\- Validated device registration 

\- Performed troubleshooting using PowerShell and Microsoft Admin Portals



\## Troubleshooting Covered



\### Hybrid Join Issues



\- SCP validation

\- Device registration troubleshooting

\- Duplicate VM identity issues

\- dsregcmd analysis



\### Entra Connect Issues



\- OU filtering

\- User synchronization

\- Computer synchronization

\- Source Anchor validation



\### Intune Enrollment Issues



\- MDM User Scope configuration

\- Intune licensing verification

\- Auto Enrollment GPO configuration

\- Device enrollment validation



\### Exchange Online



\- Custom domain verification

\- Mailbox UPN updates

\- SMTP address configuration

\- Outlook Autodiscover testing



\## Useful PowerShell Commands



```powershell

Start-ADSyncSyncCycle -PolicyType Delta

Start-ADSyncSyncCycle -PolicyType Initial

Get-ADSyncScheduler

dsregcmd /status

gpupdate /force

