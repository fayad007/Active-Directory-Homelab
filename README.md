# Active-Directory-Homelab
📌 Project Overview

Built a Windows Server Active Directory home lab to gain hands-on experience with domain administration, user management, security groups, Organizational Units, Group Policy, domain-joined computers, and access control.

The lab simulates a small organization called MYDFIR with multiple departments and users.

🎯 Objectives
Deploy and configure Active Directory Domain Services (AD DS)
Create and manage Organizational Units (OUs)
Create and manage domain users
Create and manage security groups
Configure Group Policy Objects (GPOs)
Join Windows client machines to the domain
Configure shared folders
Implement NTFS permissions
Practice common user and computer administration tasks

🏢 Lab Environment

Domain: mydfir.local

Organizational Units
mydfir.local
│
├── IT
├── HR
├── Finance
└── Operations
Users

Created 25 domain user accounts and organized them according to their respective departments.

Security Groups

Created 6 Global Security Groups:

Group	Purpose
IT_Admins	IT administrative access
IT_Support	IT support users
HR_Users	HR department access
Finance_Users	Finance department access
Operations_Users	Operations department access

Group Type: Security
Group Scope: Global

🖥️ Lab Architecture
                    MYDFIR.LOCAL
                          │
                  Windows Server
                          │
             ┌────────────┴────────────┐
             │                         │
          AD DS                       DNS
             │
      ┌──────┼──────┬──────────┐
      │      │      │          │
     IT     HR   Finance   Operations
      │      │      │          │
      └──────┴──────┴──────────┘
                    │
              Windows Client
                    │
             Domain Joined

🔧 Configuration Performed
1. Active Directory Domain Services
Installed AD DS on Windows Server
Promoted the server to a Domain Controller
Created the technova.local domain
Configured Active Directory Users and Computers

2. Organizational Units

Created four departmental OUs:

IT
HR
Finance
Operations

Users were placed into their corresponding departmental OUs.

3. User Management

Created 25 domain user accounts and configured:

Usernames
Passwords
Departmental OU placement
Group memberships
Account enable/disable settings

4. Security Groups

Created six Global Security Groups and assigned users according to their roles and access requirements.

5. Windows Client Domain Join
Configured the Windows client to use the Domain Controller for DNS
Joined the Windows client to technova.local
Logged into the client using domain accounts
Verified the computer account in Active Directory

6. Group Policy

Created and configured GPOs for basic organizational security and user management.

Configured policies such as:

Password complexity
Minimum password length
Account lockout
Automatic screen lock
Basic user restrictions

7. File Sharing & Permissions

Created departmental folders:

CompanyData
│
├── IT
├── HR
├── Finance
└── Operations

Configured NTFS permissions using security groups.

Example:

HR_Users
      ↓
   HR Folder

Finance_Users
      ↓
 Finance Folder

Operations_Users
      ↓
Operations Folder

Tested access using different domain accounts to verify that users could access only the resources assigned to their groups.

🛠️ Administrative Tasks Practiced
Creating users
Disabling and enabling accounts
Resetting passwords
Unlocking accounts
Managing group membership
Creating and managing OUs
Managing computer accounts
Joining computers to the domain
Configuring GPOs
Troubleshooting domain authentication
Managing shared-folder permissions

🧰 Technologies Used
Windows Server
Active Directory Domain Services
Active Directory Users and Computers (ADUC)
Group Policy Management
DNS
Windows 10/11
NTFS Permissions
File and Printer Sharing
Virtualization