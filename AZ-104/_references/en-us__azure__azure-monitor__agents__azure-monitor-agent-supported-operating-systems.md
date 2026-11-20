# https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-supported-operating-systems

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-supported-operating-systems

---

id="main"
 role="main"
 class="layout-body-main "
 data-bi-name="content"
 lang="en-us"
 dir="ltr"
 >
 
 
 
 
 
 Table of contents 
 
 
 
 Exit editor mode
 
 

 
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 

 

 
 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 Reading mode
 
 
 
 
 Table of contents
 
 
 
 
 
 
 Read in English
 
 
 
 
 
 
 
 Add
 
 
 
 
 
 
 Add to Plans
 
 
 
 
 
 
 
 Edit
 
 
 
 
 
 
 
 
 
 
 Copy Markdown
 
 
 
 
 
 
 Print
 
 
 
 

 
 

 
 

 

 
 
 
 
 
 
 
 
 Note
 

 
 Access to this page requires authorization. You can try signing in or changing directories.
 

 
 Access to this page requires authorization. You can try changing directories.
 

 

 

 

 
 
# Azure Monitor Agent supported operating systems and environments

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article lists the operating systems that the Azure Monitor Agent supports. For installation information, see Install and manage the Azure Monitor Agent.

Note

All operating systems listed are assumed to be x64. x86 isn't supported for any operating system.

## Windows operating systems

Operating system
Support

Windows Server 2025
â

Windows Server 2022
â

Windows Server 2022 Core
â

Windows Server 2019
â

Windows Server 2019 Core
â

Windows Server 2016
â

Windows Server 2016 Core
â

Windows 11 Client and Pro
â1, 2

Windows 11 Enterprise
(including multi-session)
â

Windows 10 1803 (RS4) and later
â1

Windows 10 Enterprise
(including multi-session) and Pro
(server scenarios only)
â

Windows 365 Cloud PCs
â1

Azure Local
â

Windows IoT Enterprise
â

1 Requires the Azure Monitor Agent client installer for Windows client devices.

2 Also supported on ARM64-based machines.

## Linux operating systems

Azure Monitor Agent supports the following Linux distributions, grouped by distribution family. Superscript numbers next to the checkmarks indicate additional notes, such as ARM64 support or prerequisite requirements. See the footnotes.

### Red Hat-based distributions

Operating system
Support 1

AlmaLinux 10
â2

AlmaLinux 9
â

AlmaLinux 8
â2

Oracle Linux 10
â2

Oracle Linux 9
â

Oracle Linux 8
â

Oracle Linux 7
â

Red Hat Enterprise Linux Server 10
â2

Red Hat Enterprise Linux Server 9+
â2

Red Hat Enterprise Linux Server 8.6+
â2

Red Hat Enterprise Linux Server 8.0-8.5
â

Red Hat Enterprise Linux Server 7.9
â

Rocky Linux 10
â2

Rocky Linux 9
â2

Rocky Linux 8
â2

### Debian-based distributions

Operating system
Support 1

Debian 13
â2

Debian 12
â2

Debian 11
â2

Debian 10
â

Debian 9
â

Ubuntu 26.04 LTS
â2

Ubuntu 24.04 LTS
â2

Ubuntu 22.04 LTS
â2

Ubuntu 20.04 LTS
â2

Ubuntu 18.04 LTS
â2

Ubuntu 16.04 LTS
â

### SUSE distributions

Operating system
Support 1

OpenSUSE 15
â

SUSE Linux Enterprise Server 16
â2

SUSE Linux Enterprise Server 15 SP7
â2

SUSE Linux Enterprise Server 12 SP5
â

### Amazon Linux

Operating system
Support 1

Amazon Linux 2
â

Amazon Linux 2023
â

### Azure Linux

Operating system
Support 1

Azure Linux 4.0
â2

Azure Linux 3.0
â2

CBL-Mariner 2.0
â2, 3

1 Requires Python (3 or 2) to be installed on the machine, including on Azure Linux and CBL-Mariner. Requires packages which and initscripts.

2 Also supported on ARM64-based machines.

3 Doesn't include the required minimum 4 GB of disk space by default. See the following note.

Note

- Machines and appliances that run heavily customized or stripped-down versions of the listed distributions and hosted solutions that disallow customization by the user aren't supported. Azure Monitor relies on various packages and other baseline functionality that these kinds of systems often remove. Installations might require some environment modifications that the appliance vendor normally disallows. For example, GitHub Enterprise Server isn't supported due to heavy customization and because of documented, license-level disallowance of operating system modification.

- Disk size in Azure Linux (previously known as CBL-Mariner) is by default lower compared to other Azure VMs, which are about 30 GB. The Azure Monitor Agent requires at least a 4-GB disk size to install and run successfully. For more information and for instructions on how to increase disk size before you install the agent, see the Azure Linux documentation.

## Hardening standards

The Azure Monitor Agent supports most industry-standard hardening standards. The product team continuously tests and certifies the agent against these standards for every release. The Azure Monitor Agent scenarios are explicitly designed for security.

### Windows hardening

The Azure Monitor Agent supports all standard Windows hardening standards, including Security Technical Implementation Guides (STIGs) and Federal Information Processing Standards (FIPS). It's also Federal Risk and Authorization Management Program (FedRAMP) compliant under Azure Monitor.

### Linux hardening

Note

Only the Azure Monitor Agent for Linux supports the hardening standards described in this section. The Dependency Agent and the Azure Diagnostics extension don't support these standards.

The Azure Monitor Agent for Linux supports various hardening standards. Each release of the agent is tested and certified against the supported hardening standards by using images that are publicly available in Azure Marketplace, including images published by Center for Internet Security (CIS). The agent supports only settings and hardening that apply to those images. It doesn't support CIS-published images that have more customizations or images customized with settings and hardening that differ from official CIS benchmarks.

Currently supported hardening standards:

- SELinux

- CIS level 1 and 21

- STIG

- FIPS

- FedRAMP

1 Only the following distributions are supported:

CIS-hardened operating system
Support

Debian 10
â

Oracle Linux 8
â

Ubuntu 18.04 LTS
â

Ubuntu 20.04 LTS
â

Red Hat Enterprise Linux Server 7
â

Red Hat Enterprise Linux Server 8
â

Red Hat Enterprise Linux Server 9
â

Important

Configuring your Linux machine system-wide crypto policy to "FUTURE" doesn't work with the Azure Monitor Agent. This policy disables certain cryptographic algorithms and prevents communication with back-end Azure Monitor services that use best-practice crypto policies. Specifically, the FUTURE policy disables some algorithms that use less than 3,072-bit keys, such as SHA-1, RSA, and Diffie-Hellman.

To identify the current policy, run the following `update-crypto-policies` command:

`sudo update-crypto-policies --show
`

## On-premises and in other clouds

You can use the Azure Monitor Agent on machines in other clouds and in on-premises environments by using Azure Arc-enabled servers. The Azure Monitor Agent authenticates to your workspace by using a managed identity. You create the managed identity when you install the Connected Machine agent, which is part of Azure Arc. The legacy Log Analytics agent authenticated by using the workspace ID and key, so it didn't need Azure Arc. Managed identity is a more secure and manageable authentication solution.

The Azure Arc agent is used only as an installation mechanism and doesn't add cost or resource consumption. Paid options for Azure Arc are available, but these options aren't required to use the Azure Monitor Agent.

## Related content

- Install the Azure Monitor Agent on Windows and Linux virtual machines.

- Identify requirements and prerequisites for Azure Monitor Agent installation.

 
 

 
 

 

 
 
 
 
 
 
## Feedback

 
 
 Was this page helpful?
 

 
 
 
 
 
 Yes
 
 
 
 
 
 No
 
 
 
 
 
 
 No
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix? 
 
 

 
 

 
 

 

 

 
 
 

 
 
 
 
## 
 Additional resources
 

 
 

 
 

 
 

 
 

 
 
 
 
 
- 
 
 Last updated on 
 2026-08-31
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
