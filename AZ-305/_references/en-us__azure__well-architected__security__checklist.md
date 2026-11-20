# https://learn.microsoft.com/en-us/azure/well-architected/security/checklist

Source: https://learn.microsoft.com/en-us/azure/well-architected/security/checklist

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
 

 

 

 

 
 
# Design review checklist for Security

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This checklist presents a set of security recommendations to help you ensure your workload is secure and aligned with the Zero Trust model. If you haven't checked the following boxes and considered the tradeoffs, then your design might be at risk. Carefully consider all of the points covered in the checklist to gain confidence in your workload's security.

## Checklist

 
Code
Recommendation

â
SE:01
Establish a security baseline that's aligned to compliance requirements, industry standards, and platform recommendations. Regularly measure your workload architecture and operations against the baseline to sustain or improve your security posture over time.

â
SE:02
Align secure development lifecycle (SDL) throughout the software development lifecycle to ensure confidentiality, integrity, and availability of software and adopt a security-first mindset.

â
SE:03
Classify and consistently apply sensitivity and information type labels on all workload data and systems involved in data processing. Use classification to influence workload design, implementation, and security prioritization.

â
SE:04
Create intentional segmentation and perimeters in your architecture design and in the workload's footprint on the platform. The segmentation strategy must include networks, roles and responsibilities, workload identities, and resource organization.

â
SE:05
Implement strict, conditional, and auditable identity and access management (IAM) across all workload users, team members, and system components. Limit access exclusively to as necessary. Use modern industry standards for all authentication and authorization implementations. Restrict and rigorously audit access that's not based on identity.

â
SE:06
Isolate, filter, and control network traffic across both ingress and egress flows. Apply defense-in-depth principles by using localized network controls at all available network boundaries across both east-west and north-south traffic.

â
SE:07
Encrypt data by using modern, industry-standard methods to guard confidentiality and integrity. Align the encryption scope with data classifications, and prioritize native platform encryption methods.

â
SE:08
Harden all workload components by reducing extraneous surface area and tightening configurations to increase attacker cost.

â
SE:09
Protect application secrets by hardening their storage and restricting access and manipulation and by auditing those actions. Run a reliable and regular rotation process that can improvise rotations for emergencies.

â
SE:10
Implement a holistic monitoring strategy that relies on modern threat detection mechanisms that can be integrated with the platform. Mechanisms should reliably alert for triage and send signals into existing SecOps processes.

â
SE:11
Establish a comprehensive testing regimen that combines approaches to prevent security issues, validate threat prevention implementations, and test threat detection mechanisms.

â
SE:12
Define and test effective incident response procedures that cover a spectrum of incidents, from localized issues to disaster recovery. Clearly define which team or individual runs a procedure.

## Next steps

We recommend that you review the Security tradeoffs to explore other concepts.

Security tradeoffs

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
