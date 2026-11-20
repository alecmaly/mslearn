# https://learn.microsoft.com/en-us/azure/well-architected/performance-efficiency/checklist

Source: https://learn.microsoft.com/en-us/azure/well-architected/performance-efficiency/checklist

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
 

 

 

 

 
 
# Design review checklist for Performance Efficiency

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This checklist presents a set of recommendations for you to scale your system so it can grow and meet your workload usage demand. The goal of performance is to maintain the efficiency of every interaction with a healthy system as demand increases. When you design and implement for performance, focus on the efficiency and effectiveness of cost, complexity, supporting new requirements, technical debt, reporting, and toil.

For every system, there's a limit to how much you can scale it without redesigning, introducing a workaround, or incorporating human involvement. If you don't include performance efficiency practices and consider the tradeoffs, your design is potentially at risk. Carefully consider all the points covered in the checklist to instill confidence in your system's success.

## Checklist

 
Code
Recommendation

â
PE:01
Define performance targets. Performance targets should be numerical values that are tied to workload requirements. You should implement performance targets for all workload flows.

â
PE:02
Conduct capacity planning. Capacity planning should be done before there are predicted changes in usage patterns, such as seasonal variations, product updates, marketing campaigns, special events, or regulatory changes.

â
PE:03
Select the right services. The services, infrastructure, and tier selections must support your ability to reach the workload's performance targets and accommodate expected capacity changes. The selections should also weigh the benefits of using platform features or building a custom implementation.

â
PE:04
Establish consistent performance measurement so behavior can be analyzed over time, compared against baselines, and used to detect degradation, inefficiency, and scaling gaps.

â
PE:05
Optimize scaling and partitioning. Incorporate reliable and controlled scaling and partitioning. The scale unit design of the workload is the basis of the scaling and partitioning strategy.

â
PE:06
Optimize your workload's performance by regularly testing in a production-like environment to ensure your workload reaches the desired performance targets and achieves your business objectives.

â
PE:07
Optimize code and infrastructure. Use code that's performant, and ensure that it offloads responsibilities to the platform. Use code and infrastructure only for their core purpose and only when necessary.

â
PE:08
Optimize data usage. Optimize data stores, partitions, and indexes for their intended and actual use in the workload.

â
PE:09
Prioritize the performance of critical flows. The allocation of workload resources and performance optimization efforts should prioritize the flows that support the most important business processes, users, and operations.

â
PE:10
Optimize operational tasks. Monitor and minimize the effects of the software development lifecycle and other routine operations on workload performance. These operations include virus scans, secret rotations, backups, reindexing databases, and deployments.

â
PE:11
Respond to live performance issues. Plan how to address performance problems by incorporating clear lines of communication and responsibilities. When a problematic situation occurs, use what you learn to identify preventive measures and incorporate them in your workload. Implement methods to return to normal operations faster when similar situations occur.

â
PE:12
Continuously optimize performance. Focus on components that show deteriorating performance over time, such as databases and networking features.

## Next steps

We recommend that you review the Performance Efficiency tradeoffs to explore other concepts.

Performance Efficiency tradeoffs

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
