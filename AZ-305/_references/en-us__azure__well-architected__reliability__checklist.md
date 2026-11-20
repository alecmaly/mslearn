# https://learn.microsoft.com/en-us/azure/well-architected/reliability/checklist

Source: https://learn.microsoft.com/en-us/azure/well-architected/reliability/checklist

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
 

 

 

 

 
 
# Design review checklist for Reliability

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This checklist presents a set of recommendations for you to use to evaluate the reliability, resiliency, and failure recovery strategies in your architecture design. To ensure reliability, identify the best infrastructure and application design for your workload. Make these decisions based on your business requirements that are mapped to availability and recoverability target metrics.

To implement a reliable design, thoroughly consider decision points in your design and be aware of how those decisions affect your workload. This checklist and the accompanying guides provide resources to help you make those decisions. Make workload reliability a central consideration throughout the workload design, development, and operation lifecycle.

## Checklist

Approach your design with a focus on reliability to help ensure that you design a workload that's resilient, manageable, and repeatable. If you don't include reliability practices and consider the tradeoffs, your design is potentially at risk. Carefully consider all the points covered in the checklist to instill confidence in your system's success.

 
Code
Recommendation

â
RE:01
Focus your workload design on simplicity and efficiency. Use a practical approach to avoid unnecessary complexity while meeting your business goals and requirements.

â
RE:02
Identify and rate user and system flows. Use a criticality scale based on your business requirements to prioritize the flows.

â
RE:03
Use failure mode analysis (FMA) to identify potential failures in your workload. Identify dependencies and failure points, and develop mitigation strategies for those failures.

â
RE:04
Define reliability and recovery targets for your workload. Use the targets to inform your design and as the foundation of your health model.

â
RE:05
Add redundancy at different levels, especially for critical flows, to help meet your reliability targets. Consider redundant infrastructure components such as compute and network, and multiple instances of your solution.

â
RE:06
Implement a timely and reliable scaling strategy at the application, data, and infrastructure levels. Base the scaling strategy on actual or predicted usage patterns and minimize manual intervention.

â
RE:07
Strengthen the resiliency of your workload by implementing self-preservation and self-healing measures. Use built-in features and well-established cloud patterns to help your workload remain functional during and recover from incidents.

â
RE:08
Test for resiliency and availability scenarios by applying the principles of chaos engineering. Use reliability testing to verify that your workload can withstand faults, scale under demand, and recover within your defined targets.

â
RE:09
Implement structured, tested, and documented disaster recovery (DR) plans that align with the recovery targets. Plans must cover all components and the system as a whole.

â
RE:10
Continuously measure and track system health using uptime and reliability indicators across components and critical flows. Ensure this data is retained and accessible to support timely detection, response, and post-incident analysis.

## Next steps

We recommend that you review the Reliability tradeoffs to explore other concepts.

Reliability tradeoffs

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-29
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
