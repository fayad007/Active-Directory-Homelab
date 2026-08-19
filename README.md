# Active-Directory-Homelab
<div align="center">

# 🖥️ Active Directory Home Lab

**A self-directed enterprise domain simulation — built to practice real-world Windows Systems Administration**

![Status](https://img.shields.io/badge/status-complete-brightgreen) ![Platform](https://img.shields.io/badge/platform-Windows%20Server-blue) ![Focus](https://img.shields.io/badge/focus-Active%20Directory-orange)

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Objectives](#-objectives)
- [Lab Environment](#-lab-environment)
- [Network & Domain Architecture](#-network--domain-architecture)
- [Organizational Structure](#-organizational-structure)
- [Group Policy Objects](#-group-policy-objects)
- [Testing & Troubleshooting](#-testing--troubleshooting)
- [Skills Demonstrated](#-skills-demonstrated)
- [Screenshots](#-screenshots)
- [Key Takeaways](#-key-takeaways)
- [Future Improvements](#-future-improvements)

---

## 📋 Overview

This project replicates a small-business IT environment on a single physical host using virtualization. The goal was to move beyond theory and get hands-on with the day-to-day tasks a **Systems Administrator** or **IT Support Specialist** performs: provisioning accounts, organizing them logically, enforcing policy centrally, and troubleshooting the kind of issues that come up in a live domain.

Everything in this lab was built, configured, and tested end-to-end — from promoting a bare Windows Server to a Domain Controller, through to simulating and resolving real authentication and policy failures.

---

## 🎯 Objectives

- [x] Stand up a functioning Active Directory domain from scratch
- [x] Design a realistic organizational structure (OUs, groups, users)
- [x] Enforce security and usability policy via Group Policy
- [x] Configure core network services (DNS, DHCP)
- [x] Join client machines to the domain and validate policy application
- [x] Deliberately break and repair common domain issues to build troubleshooting reps

---

## 🧰 Lab Environment

| Component | Details |
|---|---|
| Hypervisor | * VirtualBox * |
| Domain Controller | Windows Server *(version)* |
| Client machine | *( Windows 10/11 )* |
| Domain name | *(e.g. corp.local)* |
| Domain users | 25 |
| Security groups | 6 |
| Organizational Units | 4 |
| Group Policy Objects | 5 |
| Domain-joined clients | 3 |

---

## 🌐 Network & Domain Architecture

```
                        ┌────────────────────────┐
                        │   Windows Server (DC)   │
                        │  Active Directory DS    │
                        │  DNS  +  DHCP           │
                        └────────────┬────────────┘
                                     │
                     ┌───────────────┼───────────────┐
                     │               │               │
             ┌───────▼──────┐ ┌──────▼───────┐ ┌─────▼────────┐
             │  Client PC 1  │ │  Client PC 2  │ │  Client PC 3  │
             │(Domain-Joined)│ │(Domain-Joined)│ │(Domain-Joined)│
             └───────────────┘ └───────────────┘ └───────────────┘
```

*(Replace with a real network diagram export from your hypervisor or a tool like draw.io once available — see [Screenshots](#-screenshots).)*

---

## 🗂️ Organizational Structure

The domain is organized into 4 OUs mapped to business functions, with 6 security groups nested underneath for permission and policy targeting.

```
corp.local
│
├── OU: Finance
│   └── Group: Finance_Users
│       └── Finance staff accounts
│
├── OU: Operations
│   └── Group: Operations_Users
│       └── Operations staff accounts
│
├── OU: HR
│   └── Group: HR_Users
│       └── HR staff accounts
│
└── OU: IT
    ├── Group: IT_Admins
    │   └── Domain administrators
    ├── Group: IT_Support
    │   └── Helpdesk / support staff
    └── Group: VPN_Users
        └── Remote access accounts
```

**25 user accounts** were provisioned across these OUs/groups, reflecting a realistic small-business headcount and department split.

---

## 🛡️ Group Policy Objects

5 GPOs were designed and deployed for centralized administration:

```
Group Policy Objects (5)
│
├── Password & Account Lockout Policy
│   ├── Minimum password length enforced
│   ├── Password complexity requirements enabled
│   └── Account lockout threshold & duration configured
│
├── Restrict Control Panel Access
│   └── Prevents standard users from modifying system settings
│
├── Drive Mapping
│   └── Auto-maps network drives per department/OU on login
│
├── Disable USB Devices
│   └── Blocks USB storage access for endpoint security
│
└── Desktop Wallpaper Enforcement
    └── Applies standardized wallpaper across domain clients
```

| GPO | Purpose | Linked To |
|---|---|---|
| Password & Account Lockout Policy | Enforces password complexity, minimum length, and lockout after failed logins | Domain-wide |
| Restrict Control Panel Access | Blocks standard users from system settings | All user OUs |
| Drive Mapping | Maps department drives automatically on login | Per-OU |
| Disable USB Devices | Blocks USB storage devices | Domain-wide |
| Desktop Wallpaper Enforcement | Standardizes desktop appearance | Domain-wide |

---

## 🧪 Testing & Troubleshooting

Rather than just configuring policy and walking away, each GPO and service was **deliberately tested** to confirm real enforcement — and several failure scenarios were induced and resolved to build practical troubleshooting reps.

| # | Scenario | Action Taken | Resolution |
|---|---|---|---|
| 1 | Password complexity/length enforcement | Attempted non-compliant password changes | Confirmed policy rejected weak passwords as expected |
| 2 | Account lockout behavior | Triggered repeated failed logins | Confirmed lockout after threshold; unlocked via Active Directory Users and Computers |
| 3 | USB device restriction | Attempted to mount USB storage on a domain client | Confirmed device access blocked by GPO |
| 4 | Control Panel restriction | Attempted to access system settings as standard user | Confirmed access denied |
| 5 | Drive mapping | Logged in as users in different OUs | Confirmed correct network drives mapped automatically per department |
| 6 | Authentication failures | Simulated invalid credential scenarios | Diagnosed via Event Viewer, resolved via account/policy review |
| 7 | DNS resolution errors | Simulated broken name resolution on a client | Traced to DNS misconfiguration, corrected on DC |
| 8 | Permission issues | Simulated denied access to shared resources | Resolved via NTFS/share permission audit |

---

## 🧠 Skills Demonstrated

- Active Directory Domain Services (AD DS) design and deployment
- User, group, and OU administration
- Group Policy creation, deployment, and centralized enforcement
- Password policy configuration: complexity, minimum length, account lockout threshold/duration
- DNS/DHCP configuration in a Windows Server environment
- Domain client join and policy validation
- Systematic troubleshooting: authentication failures, account lockouts, DNS errors, permission issues

---

## 📸 Screenshots

> ⚠️ **Add your real screenshots here** — this is the single highest-impact section for a hiring manager, since it turns every claim above into visible proof. Suggested shots:

| Screenshot | What to Capture |
|---|---|
| `screenshots/ad-users-and-computers.png` | Active Directory Users and Computers — full OU/group tree |
| `screenshots/gpo-password-policy.png` | Password & Account Lockout GPO settings |
| `screenshots/gpo-usb-restriction.png` | USB device restriction GPO settings |
| `screenshots/domain-join-success.png` | A client machine successfully joined to the domain |
| `screenshots/account-lockout-test.png` | Account lockout triggered after failed logins |
| `screenshots/gpresult-output.png` | `gpresult /r` output confirming applied policies on a client |
| `screenshots/dns-dhcp-config.png` | DNS/DHCP configuration on the Domain Controller |

Once added, embed them like this:

```markdown
![AD Users and Computers](screenshots/ad-users-and-computers.png)
```

---

## 💡 Key Takeaways

*(Add 2–3 sentences in your own words — what surprised you, what was harder than expected, or what you'd do differently on a second pass. This section is what separates a checklist from a reflection, and hiring managers notice the difference.)*

---

## 🚀 Future Improvements

- [ ] Add a second Domain Controller for redundancy testing
- [ ] Implement fine-grained password policies (per-OU rather than domain-wide)
- [ ] Integrate a SIEM (e.g. Wazuh) to monitor and alert on the simulated failure scenarios above
- [ ] Automate user/group provisioning with PowerShell instead of manual creation
- [ ] Document a full disaster-recovery test (DC failure/restore)

---

<div align="center">

*Part of a broader self-directed IT infrastructure learning track, alongside a Windows Troubleshooting Lab and SpiceWorks ticketing practice.*

</div>