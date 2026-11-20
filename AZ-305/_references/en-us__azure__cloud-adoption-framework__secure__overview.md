# https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/secure/overview

Source: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/secure/overview

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
 

 

 

 

 
 
# Secure overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The Cloud Adoption Framework for Azure Secure methodology provides a structured approach for securing your Azure cloud estate. This overview introduces security guidance that applies across every methodology phase of the Cloud Adoption Framework. Security spans strategy, planning, readiness, adoption, governance, and operations; gaps in any phase weaken overall posture. You should apply the Secure methodology end to end so every phase decision reinforces protection, detection, and resilience.

## Modernize security posture

Security posture modernization is the continuous elevation of your defenses, detections, and resilience capabilities. This modernization matters here because static controls degrade quickly against evolving attacker tradecraft. You should align modernization work with the Microsoft Zero Trust adoption framework and enrich each phase task with Zero Trust improvements.

Integrate identity strengthening, segmentation, just-in-time and least-privilege access, threat detection tuning, data protection, and platform baseline automation into your landing zones and operations. Prioritize modernization sprints based on measurable risk reduction (for example, exposed privileges, insecure configurations, unmonitored assets). Automate validation through policy, infrastructure as code, continuous compliance scanning, and secure score tracking in Microsoft Defender for Cloud.

## Prepare for and respond to incidents

Incident preparation and response form a primary control layer that limits attacker dwell time and business disruption. This capability matters because even mature preventive controls can't eliminate intrusion attempts. You should implement and continuously improve an end-to-end incident lifecycle covering readiness, detection, triage, containment, eradication, recovery, and post-incident learning.

Codify roles, communication channels, evidence handling, and decision authority. Instrument telemetry ingestion and alert fidelity improvements to cut false positives and accelerate mean time to detect (MTTD). Use Azure incident response guidance to refine runbooks, practice tabletop simulations, and automate containment actions (for example, isolate hosts, revoke tokens, quarantine storage) through orchestrated workflows.

## Adopt CIA Triad principles

CIA Triad principles (confidentiality, integrity, availability) provide a concise model for comprehensive information protection. This model matters here because gaps in any single principle create cascading weaknesses. You should map controls, processes, telemetry, and metrics explicitly to each principle for every phase.

- Confidentiality restricts access to sensitive data; encryption, key management, identity, access policies, network segmentation, and data classification controls enforce it.

- Integrity preserves data correctness and completeness; hashing, signing, immutable storage patterns, version control, and secure update supply chains enforce trustworthy state.

- Availability maintains timely access to services and data; redundancy design, fault domain isolation, autoscaling, health probes, chaos testing, backup, and disaster recovery orchestration sustain accessibility.

Apply the triad to drive:

- Data protection: Map sensitivity labels and encryption controls to confidentiality risk.

- Business continuity: Engineer integrity and availability safeguards to sustain operations.

- Stakeholder confidence: Demonstrate measurable adherence to each principle in audits and compliance reporting.

Each article surfaces tasks that address confidentiality, integrity, and availability so you can embed these principles into strategy, design, build, governance, and operations.

## Sustain security posture

Security posture sustainment is the disciplined cycle of measuring, improving, and validating control efficacy. This sustainment matters because threat actors iterate rapidly and static defenses lose relevance. You should institutionalize recurring assessment, prioritized remediation, control automation, and evidence-based reporting.

Track secure score security controls in Microsoft Defender for Cloud to quantify gaps, and couple them with risk-based metrics (for example, exposure of high-privilege identities or unencrypted sensitive stores). Automate drift detection through policy, configuration baselines, and deployment pipelines. Feed incident retrospectives and threat intelligence into backlog refinement so posture change aligns with live adversary behaviors.

## Use the cloud security checklist

The cloud security checklist is a consolidated navigation and tracking aid for Secure methodology execution. This checklist matters because it reduces omission risk, accelerates onboarding, and supports audit readiness. You should integrate it into team working agreements and progress reviews as the authoritative task register.

 
Cloud security step
Cloud security tasks

â
Understand security teams and roles.
â Understand the role of the cloud service provider. 
 â Understand the roles of Infrastructure and Platform teams. 
 â Understand the roles of Security architecture, engineering, posture management teams. 
 â Understand the roles of the Security Operations (SecOps and SOC) teams. 
 â Understand the roles of Security Governance, Risk, and Compliance (GRC) teams. 
 â Learn about security education and policy.

â
Integrate security into your cloud adoption strategy.
â Security posture modernization strategy. 
 â Incident preparedness and response strategy. 
 â Confidentiality strategy. 
 â Integrity strategy. 
 â Availability strategy. 
 â Security posture sustainment strategy

â
Plan for a secure cloud adoption.
â Plan for landing zone adoption. 
 â Security posture modernization planning. 
 â Incident preparedness and response planning. 
 â Confidentiality planning. 
 â Integrity planning 
 â Availability planning 
 â Security posture sustainment planning

â
Ready your secure cloud estate.
â Ready for security posture modernization. 
 â Ready for incident preparedness and response. 
 â Ready for confidentiality. 
 â Ready for integrity. 
 â Ready for availability 
 â Ready for security posture sustainment

â
Perform your cloud adoption securely.
â Security posture modernization adoption. 
 â Adopt incident preparedness and response. 
 â Adopt confidentiality. 
 â Adopt integrity. 
 â Adopt availability. 
 â Adopt security posture sustainment

â
Securely govern your cloud estate.
â Security posture modernization. 
 â Incident preparedness and response governance 
 â Confidentiality governance. 
 â Integrity governance. 
 â Availability governance. 
 â Sustaining security governance

â
Securely manage your cloud estate.
â Security posture modernization. 
 â Managing incident preparedness and response 
 â Managing confidentiality. 
 â Managing integrity. 
 â Managing availability. 
 â Managing security sustainment

## Next step

Security teams, roles, and functions

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
