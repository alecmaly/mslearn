# https://learn.microsoft.com/en-us/security/zero-trust/zero-trust-overview

Source: https://learn.microsoft.com/en-us/security/zero-trust/zero-trust-overview

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
 

 

 

 

 
 
# Zero Trust as a security foundation

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Zero Trust provides a modern security foundation for designing, implementing, and operating security across an organization. It helps organizations operate securely in complex environments where users, devices, applications, workloads, data, and infrastructure are distributed across organizational and technology boundaries.

Zero Trust is often summarized as "never trust, always verify." This phrase is a useful reminder not to grant access or assume something is safe solely because of its location, ownership, or previous trust. In practice, Zero Trust means making security decisions explicitly, using available context and risk information, limiting unnecessary privileges and dependencies, and designing for the possibility of compromise.

These ideas extend beyond individual access decisions. They influence how organizations design architectures, protect assets, operate security controls, monitor environments, respond to threats, and limit the impact when something is compromised.

## Zero Trust principles

Microsoft Zero Trust guidance uses three principles that shape sedcurity decisions across the organization and security controls across AI, identities, devices, applications, workloads, data, infrastructure, networks.

Principle
Application

Assume compromise (previously referred to as assume breach)
Design and operate on the expectation that attackers might gain access to part of the environment. Limit potential impact and support rapid detection, response, and recovery.

Verify explicitly
Make security and access decisions using relevant identity, device, resource, environmental, behavioral, and risk signals rather than relying on implicit trust.

Use least privilege access
Limit access and control relationships to what is required, for only as long as required, reducing unnecessary exposure and potential blast radius.

Together, these principles help organizations make deliberate trust decisions rather than inheriting trust from network location, organizational boundaries, or previous interactions.

## Zero Trust outcomes

When applied consistently, Zero Trust leads to clear, consistent, and measurable security outcomes that replace traditional "trust-by-default" models with "trust-by-exception".

This produces several important security outcomes:

- Trust decisions are explicit and context-aware: Security decisions use relevant context and telemetry rather than relying on location or other implicit indicators of trust.

- Access is conditional and temporary: Permissions and control relationships are limited to what users, workloads, and systems need to perform their intended functions.

- Privileges can adapt as conditions change: Access and security decisions can be reassessed when identity, device, behavior, environment, or risk conditions change.

- Potential blast radius is reduced: Segmentation, least privilege, and constrained control relationships limit how far an attacker can move after compromise.

- Security controls operate across environments: Principles and controls apply across on-premises systems, cloud platforms, SaaS applications, operational environments, and AI workloads.

- Detection, response, and recovery are part of the design: Organizations monitor for compromise and prepare to contain, remediate, and recover when preventive controls don't stop an attack.

Zero Trust therefore isn't an expectation that compromise can always be prevented. It combines prevention with deliberate preparation for detecting and limiting compromise when it occurs.

## Zero Trust and security graph thinking

A graph is a model of entities (nodes) and their relationships. A security graph helps teams understand which entities can access or control other entities, such as users, devices, apps, identities, and resources.

Threat actors abuse these control relationships during attacks. In most attacks, adversaries move across existing relationships rather than breaking every control directly. If an upstream entity is compromised, downstream entities it controls can also be compromised.

This dynamic is amplified by two realities:

- Transitive control relationships: If A controls B and B controls C, A effectively controls C.

- Low-friction access for productivity: Organizations intentionally enable broad access paths to support fast work, which can also increase attacker reach if not governed tightly.

The three Zero Trust principles reduce this risk by shaping both system-level strategy and per-relationship controls.

### Apply assume compromise and business enablement together

Organizations must achieve business outcomes while operating safely in environments where attacks and failures can occur. Assume compromise establishes this security reality as a design constraint, while business enablement ensures that security supports rather than unnecessarily obstructs the organization's mission.

Together, these ideas encourage organizations to design systems that enable necessary business activity while limiting the likelihood and impact of compromise.

### Apply verify explicitly and least privilege per relationship

The other two principles apply to each entity and its inbound and outbound control paths:

- Verify explicitly reduces attack surface by validating trust decisions with all relevant context and telemetry.

- Least privilege reduces blast radius by limiting standing access and unnecessary control relationships.

Depending on the technology and scenario, these principles can be implemented through approaches such as:

- Just-enough access (JEA) for role-scoped authorization.

- Just-in-time access (JIT) for time-bounded elevation.

- Risk-based policy enforcement and reassessment as conditions change.

- Segmentation and isolation that constrain potential attack paths.

- Monitoring and detection that identify unexpected or malicious behavior.

## Challenging traditional assumptions

Many traditional security approaches relied heavily on network boundaries and treated systems or activity inside a trusted perimeter differently from those outside it.

Those controls remain useful, but network location alone is no longer a sufficient basis for trust. Modern environments span cloud services, endpoints, identities, applications, data, infrastructure, operational technology, and AI workloads. Attackers can also use legitimate credentials, sessions, applications, tools, and administrative relationships to move through these environments.

Zero Trust challenges implicit trust by:

- Making trust decisions explicitly instead of inheriting them from location or ownership.

- Using current context and risk to inform security decisions.

- Limiting privileges and control relationships to reduce attack paths and blast radius.

- Designing for detection, containment, response, and recovery when compromise occurs.

- Treating security as an organizational responsibility supported by technology, people, and processes.

## Key shifts

Applying Zero Trust principles drives several broader shifts in how organizations approach security:

Protection follows the asset and its relationships

Assets aren't inherently protected because of where they reside. Protect them based on their value, sensitivity, exposure, dependencies, and relationships with other entities.

- Trust is explicit and contextual

Don't assume that an identity, device, workload, network connection, or other entity should be trusted simply because of its location, ownership, or previous activity. Use relevant information to make security decisions.

- Privilege and control relationships are constrained

Reduce unnecessary standing privilege and limit the paths through which compromise of one entity can affect others.

- Compromise is anticipated

Prevent attacks where possible, while also designing controls and operations to detect, contain, respond to, and recover from compromise.

- Security includes technology, people, and processes

Technical controls alone can't address every source of risk. Human behavior, operational practices, architecture, processes, and technology all influence security outcomes.

- Security enables business outcomes

Zero Trust doesn't seek to eliminate access, connectivity, or collaboration. It enables organizations to provide the access and functionality the business needs while deliberately managing the associated security risk.

## Apply Zero Trust principles with SAF

Adopting Zero Trust is an incremental ongoing effort. Every organization starts from a different place based on its business priorities, risk profile, security maturity, technology environment, and existing investments.

The Microsoft Security Adoption Framework (SAF) uses Zero Trust as a foundational set of security principles rather than treating it as a single technology architecture or implementation project. SAF connects these principles with business priorities, security practices, and technical implementation.

SAF does this through three complementary components:

- Business scenarios

Help leaders identify and prioritize important security outcomes based on business and security risk.

- Security disciplines

Help teams build the strategy, architecture, processes, capabilities, and operational practices required to achieve those outcomes.

- Technology pillars

Apply security principles to technology areas such as identity, endpoints, applications, data, infrastructure, networks, and AI workloads.

## Next steps

- To get started with structured adoption, follow our SAF journey.

- To dive into critical security outcomes, start with our business scenarios.

- To begin with assessment of your current Zero Trust posture, start Zero Trust assessment.

- To dive directly into implementation, review implementing technical solutions.

- For standards and framework mappings, start with Security standards and frameworks.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
