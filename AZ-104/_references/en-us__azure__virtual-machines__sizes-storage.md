# https://learn.microsoft.com/en-us/azure/virtual-machines/sizes-storage

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/sizes-storage

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
 

 

 

 

 
 
# Sizes for virtual machines in Azure

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: âï¸ Linux VMs âï¸ Windows VMs âï¸ Flexible scale sets âï¸ Uniform scale sets

Azure Virtual Machine (VM) sizes are designed to provide a wide range of options for hosting your servers and their workloads in the cloud. Sizes are categorized into different families and types, each optimized for specific purposes. Users can choose the most suitable VM size based on their requirements, such as CPU, memory, storage, and network bandwidth.

This article describes what sizes are, gives an overview of the available sizes and shows different options for Azure virtual machine instances you can use to run your apps and workloads.

## VM size and series naming

Azure VM sizes follow specific naming conventions to denote varying features and specifications. Each character in the name represents different aspects of the VM. These include the VM family, number of vCPUs, and extra features like premium storage or included accelerators.

VM naming is further broken down into the 'Series' name and the 'Size' name. Size names include extra characters representing the number of vCPUs, type of storage, etc.

Category
Description
Links

Type
Basic categorization by intended workload.
General purpose 
Compute optimized 
Memory optimized 
Storage optimized 
GPU accelerated 
FPGA accelerated

Series
Group of sizes with similar hardware and features.
Enter the 'Series' tab here.

Size
Specific VM configuration, including vCPUs, memory, and accelerators.
Enter the 'Size' tab here.

### Name structure breakdown

- 
Series

- 
Size

Here's a breakdown of a 'General purpose, DCads_v5-series' size series.

1 Most families are represented using one letter, but others such as GPU sizes (`ND-series`, `NV-series`, etc.) use two.

2 Most subfamilies are represented with a single upper case letter, but others (such as `Ebsv5-series`) are still considered subfamilies of their parent family due to feature differences.

3 If no feature letter for a CPU is listed, the series uses Intel x86-64 CPUs. If the CPU is AMD, it's listed as `a`. If the CPU is ARM based (Microsoft Cobalt or Ampere Altra), it's listed as `p`.

4 There can be any number of extra features in a size name. There could be none (`Dv5-series`) or there could be three (`Dplds_v6-series`).

5 Version numbers only appear in the size name if there are multiple versions of the same series. If you're using the first version of a series (`HB-series`, `B-series`, etc.) it's often not included in the size name.

Note

Not all sizes will have subfamilies, support accelerators, or specify the CPU vendor. For more information on VM size naming conventions, see Azure VM sizes naming conventions.

Here's a breakdown of a 'Standard_DC8ads_v5' size in the 'DCadsv5-series'

1 Most families are represented using one letter, but others such as GPU sizes (`ND-series`, `NV-series`, etc.) use two.

2 Most subfamilies are represented with a single upper case letter, but others (such as `Ebsv5-series`) are still considered subfamilies of their parent family due to feature differences.

3 If no feature letter for a CPU is listed, the series uses Intel x86-64 CPUs. If the CPU is AMD, it will be listed as `a`. If the CPU is ARM based (Microsoft Cobalt or Ampere Altra), it will be listed as `p`.

4 There can be any number of extra features in a size name. There could be none (`Dv5-series`) or there could be three (`Dplds_v6-series`).

5 Spacers can show up multiple times in a size name such as in the `ND_H100_v5-series`. In this case they separate the GPU ID from the rest of the size name.

6 Version numbers only appear in the size name if there are multiple versions of the same series. If you're using the first version of a series (`HB-series`, `B-series`, etc.) it's often not included in the size name.

Note

Not all sizes will have subfamilies, support accelerators, or specify the CPU vendor. For more information on VM size naming conventions, see Azure VM sizes naming conventions.

## List of VM size families by type

This section contains a list of all current generation size series with tabs dedicated to each size family. Each group has a 'Series List' column with a linked list of all available size series, These links will bring you to the family page for that series, where you can find detailed information on each size in that series or go to the series' page for a list of sizes in that series.

To learn more about a size family, select the 'family' tab under each type section. There you can read a summary on the family, see the workloads it's recommended for, and view the full family page with specifications for all series in that family.

### General purpose

General purpose VM sizes provide balanced CPU-to-memory ratio. Ideal for testing and development, small to medium databases, and low to medium traffic web servers.

- 
Family list

- 
A family

- 
B family

- 
D family

- 
DC family

Family
Workloads
Series List

A-family
Entry-level economical
Av2-series 
 End of Life A-family series

B-family
Burstable
Bsv2-series 
 Basv2-series 
 Bpsv2-series 
End of Life B-family series

D-family
Enterprise-grade applications 
 Relational databases 
 In-memory caching 
 Data analytics
Dpsv7 and Dpdsv7-series 
 Dplsv7 and Dpldsv7-series 
 Dsv7 and Ddsv7 series 
 Dlsv7 and Dldsv7 series 
 Dasv7 and Dadsv7 series 
 Dalsv7 and Daldsv7 series 
 Dpsv6 and Dplsv6-series 
 Dpdsv6 and Dpldsv6-series 
 Dasv6 and Dadsv6-series 
 Dalsv6 and Daldsv6-series 
 Dsv6 and Ddsv6-series 
 Dlsv6 and Dldsv6-series 
 Dpsv5 and Dpdsv5-series 
 Dplsv5 and Dpldsv5-series 
 Dlsv5 and Dldsv5-series 
 Dv5 and Dsv5-series 
 Ddv5 and Ddsv5-series 
 Dasv5 and Dadsv5-series 
 End of Life D-family series

DC-family
D-family with confidential computing
DCasv5 and DCadsv5-series 
 DCas_cc_v5 and DCads_cc_v5-series 
 DCesv6-series 
 DCedsv6-series 
 DCasv6 and DCadsv6-series 
 DCsv3 and DCdsv3-series 
 End of Life DC-family

##### A family

The 'A' family of VM size series are one of Azure's general purpose VM instances. They're designed for entry-level workloads, such as development and test environments, small to medium databases, and low-traffic web servers.

View the full A family page

Cost Efficiency: A-series VMs are some of the most budget-friendly options available on Azure, making them a good choice for projects with limited financial resources or those that do not require high-performance compute capabilities.

General Workloads: A-series VMs are well-suited for handling basic applications, light web servers, and small databases that do not demand extensive CPU, memory, or I/O performance.

Entry-Level Applications: A-series VMs can serve as a good starting point for deploying applications that are not expected to scale significantly. They provide a platform for applications and services that require less processing power.

##### B family

The 'B' family of VM size series are one of Azure's general purpose VM instances. While traditional Azure virtual machines provide fixed CPU performance, B-series virtual machines are the only VM type that use credits for CPU performance provisioning. B-series VMs utilize a CPU credit model to track how much CPU is consumed - the virtual machine accumulates CPU credits when a workload is operating below the base CPU performance threshold and uses credits when running above the base CPU performance threshold until all of its credits are consumed. Upon consuming all the CPU credits, a B-series virtual machine is throttled back to its base CPU performance until it accumulates the credits to CPU burst again.

View the full B family page

Usage Flexibility: B-family VMs are best suited for workloads that do not require constant full CPU performance.

Ideal Applications: B-family VMs are ideal applications include web servers, proof of concepts, small databases, and development build environments.

Performance Needs: Some workloads often have burstable performance requirements, meaning they only need high performance sporadically. B-family VMs are perfect for this use case.

##### D family

The 'D' family of VM sizes are one of Azure's general purpose VM sizes. They're designed for a variety of demanding workloads, such as enterprise applications, web and application servers, development and test environments, and batch processing tasks. Equipped with faster processors and more memory per core than the A-series, D-series VMs offer a strong performance balance, making them suitable for applications that require both high computational power and substantial memory resources. They are particularly favored for running enterprise-grade applications, supporting moderate to high-traffic web servers, and performing data-intensive batch processing.

View the full D family page

Balanced Performance: D-series VMs provide a solid balance between CPU capabilities and memory size, which makes them suitable for most production workloads. They are equipped with faster processors compared to the A-series and provide more memory per core.

Enterprise Applications: They are well-suited for running enterprise applications like SAP, Microsoft Dynamics, or large relational databases that require both high computational power and substantial memory.

Development and Test Environments: With their balanced resources, D-series VMs are ideal for development and testing environments where developers need to simulate production conditions closely.

Web and Application Servers: They provide the necessary resources to host web servers and application servers that experience moderate to heavy traffic, ensuring smooth and responsive user experiences.

Batch Processing: D-series VMs are efficient for handling batch processing tasks that require processing large amounts of data quickly, thanks to their fast processors and ample memory.

Gaming Servers: The high-performance capabilities of D-series VMs make them suitable for gaming servers where latency and speed are critical for a good user experience.

##### DC family

The 'DC' series family are one of Azure's security focused general purpose VM instances. They're designed for confidential computing offering enhanced data protection and integrity with various hardware-based Trusted Execution Environments (TEEs). These VMs work well for many general computing workloads, e-commerce systems, web front ends, desktop virtualization solutions, sensitive databases, other enterprise applications and more.

View the full DC family page

Data Protection: DC-series VMs are ideal for applications that manage, store, and process sensitive data, such as personal identifiable information (PII), financial data, health records, and other types of confidential information. The hardware-based encryption ensures that data is protected at rest and during processing.

Regulatory Compliance: For businesses that need to comply with stringent regulatory requirements for data privacy and security (like GDPR, HIPAA, or financial industry regulations), DC-series VMs provide a hardware-assured environment that can help meet these compliance demands.

### Compute optimized

Compute optimized VM sizes have a high CPU-to-memory ratio. These sizes are good for medium traffic web servers, network appliances, batch processes, and application servers.

- 
Family list

- 
F family

- 
FX family

List of compute optimized VM size families:

Family
Workloads
Series List

F-family
Medium traffic web servers 
 Network appliances 
 Batch processes 
 Application servers
Fasv7 and Fadsv7 series 
 Famsv7 and Famdsv7 series 
 Falsv7 and Faldsv7 series 
 Fasv6, Falsv6, and Famsv6-series 
 Fsv2-series 
 End of Life F-family

FX-family
Electronic Design Automation (EDA) 
 Large memory relational databases 
 Medium to large caches 
 In-memory analytics
FX-series 
 FXmsv2-series 
 FXmdsv2-series

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

##### F family

The 'F' family of VM size series are one of Azure's compute-optimized VM instances. They're designed for workloads that require high CPU performance, such as batch processing, web servers, analytics, and gaming. Featuring a high CPU-to-memory ratio, F-series VMs are equipped with powerful processors to handle applications that demand more CPU capacity relative to memory. This makes them particularly effective for scenarios where fast and efficient processing is critical, allowing businesses to run their compute-bound applications efficiently and cost-effectively.

View the full F family page

Web Servers: F-series VMs are excellent for hosting web servers and applications that require significant compute capability to handle web traffic efficiently without necessarily needing large amounts of memory.

Batch Processing: F-series VMs are ideal for batch jobs and other processing tasks that involve handling large volumes of data or tasks in a queue but are more CPU-intensive than memory-intensive.

Application Servers: Applications that require quick processing and do not have high memory demands can benefit from F-series VMs. These can include medium traffic application servers, back-end servers for enterprise applications, and other similar tasks.
Gaming Servers: Due to their high CPU performance, F-series VMs are also suitable for gaming servers where fast processing is critical for a good gaming experience.

Analytics: F-series VMs can be used for data analytics applications that require processing speed to crunch numbers and perform calculations more than they require a large amount of memory.

##### FX family

The 'FX' family of VM size series are one of Azure's specialized compute-optimized VM instances, designed primarily workloads that require significant CPU capabilities. These VMs use the latest Intel Ice Lake processors and are optimized for compute-intensive tasks such as financial modeling, scientific simulations, and heavy calculations. With a high frequency and a large cache per core, FX-series VMs provide exceptional computational power, making them ideal for scenarios demanding extensive processing resources and rapid execution of complex operations.

View the full FX family page

Electronic Design Automation (EDA): FX-series VMs are well-suited for EDA workloads, which require high CPU clock speeds and high memory-to-CPU ratios. These workloads benefit from the high single-core performance and large memory capacity of FX-series VMs.

Batch Processing: FX-series VMs are excellent for high-throughput batch processing jobs, such as those involving large-scale data analysis and transformation, where rapid processing is critical.

Data Analytics: FX-series VMs are suitable for intensive data analytics applications, especially those that require quick iteration and processing of large data sets.

### Memory optimized

Memory optimized VM sizes offer a high memory-to-CPU ratio that is great for relational database servers, medium to large caches, and in-memory analytics.

- 
Family list

- 
E family

- 
Eb family

- 
EC family

- 
M family

List of memory optimized VM sizes with links to each series' family page section:

Family
Workloads
Series List

E-family
Relational databases 
 Medium to large caches 
 In-memory analytics
Epsv7 and Epdsv7-series 
 Esv7 and Edsv7-series 
 Easv7 and Eadsv7 series 
 Esv6 and Edsv6-series 
 Epsv6 and Epdsv6-series
 Easv6 and Eadsv6-series
 Ev5 and Esv5-series
 Edv5 and Edsv5-series
 Easv5 and Eadsv5-series
 Epsv5 and Epdsv5-series
 End of Life families

Eb-family
E-family with High remote storage performance
Ebsv6 and Ebdsv6-series 
 Ebdsv5 and Ebsv5-series

EC-family
E-family with confidential computing
ECasv6 and ECadsv6-series
 ECasv5 and ECadsv5-series
 ECas_cc_v5 and ECads_cc_v5-series

M-family
Extremely large databases 
 Large amounts of memory
Mpsv4 and Mpdsv4-series 
 Mbsv3 and Mbdsv3-series
 Msv3 and Mdsv3 Medium Memory series
 Msv3 and Mdsv3 High Memory series
 Mdsv3 Very High Memory series 
 Msv2 and Mdsv2-series 
 Msv2 High Memory Series
 M-series

Other families
Older generation memory optimized sizes
Dnsv6 and Dndsv6-series 
 Dnlsv6 and Dnldsv6-series 
 Ensv6 and Endsv6-series 
 End of Life families

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

##### E family

The 'E' family of VM size series are one of Azure's memory-optimized VM instances. They're designed for memory-intensive workloads, such as large databases, big data analytics, and enterprise applications that require significant amounts of RAM to maintain high performance. Equipped with high memory-to-core ratios, E-series VMs support applications and services that benefit from faster data access and more efficient data processing capabilities. This makes them particularly well-suited for scenarios involving in-memory databases and extensive data processing tasks where ample memory is crucial for optimal performance.

View the full E family page

Memory-Intensive Workloads: E-family VMs are for workloads that demands a large memory footprint to efficiently handle tasks, such as simulations, large-scale computations in scientific research, or financial risk modeling.

Large Databases and SQL Servers: E-family VMs are ideal for hosting large relational databases like SQL Server and NoSQL databases that benefit from high memory capacities for improved performance in data processing and transaction handling.

Enterprise Applications: E-family VMs are suitable for resource-intensive enterprise applications, including large-scale ERP and CRM systems, where the availability of ample memory is crucial for managing complex transactions and user loads.

Big Data Applications: E-family VMs are effective for big data analytics applications that need to process vast amounts of data in memory to speed up analysis and insights generation.

In-Memory Computing: E-family VMs are great for in-memory databases (e.g., SAP HANA) that require large amounts of RAM to keep the entire dataset in memory, allowing for ultra-fast data processing and query responses.

Data Warehousing: E-family VMs provide the necessary resources for data warehousing solutions that handle and analyze large datasets, improving query performance and reducing response times.

##### Eb family

The 'Eb' family of VM size series are one of Azure's memory-optimized VM instances. They're designed for memory-intensive workloads with high remote storage performance, such as large databases, big data analytics, and enterprise applications that require significant amounts of RAM to maintain high performance. Equipped with high memory-to-core ratios, Eb-series VMs support applications and services that benefit from faster data access and more efficient data processing capabilities. This makes them particularly well-suited for scenarios involving in-memory databases and extensive data processing tasks where ample memory is crucial for optimal performance.

View the full Eb family page

Memory-Intensive Workloads: Eb-family VMs are for workloads that demand a large memory footprint to efficiently handle tasks, such as simulations, large-scale computations in scientific research, or financial risk modeling.

Large Databases and SQL Servers: Eb-family VMs are ideal for hosting large relational databases like SQL Server and NoSQL databases that benefit from high memory capacities for improved performance in data processing and transaction handling.

Enterprise Applications: Eb-family VMs are suitable for resource-intensive enterprise applications, including large-scale ERP and CRM systems, where the availability of ample memory is crucial for managing complex transactions and user loads.

Big Data Applications: Eb-family VMs are effective for big data analytics applications that need to process vast amounts of data in memory to speed up analysis and insights generation.

In-Memory Computing: Eb-family VMs are great for in-memory databases (e.g., SAP HANA) that require large amounts of RAM to keep the entire dataset in memory, allowing for ultra-fast data processing and query responses.

Data Warehousing: Eb-family VMs provide the necessary resources for data warehousing solutions that handle and analyze large datasets, improving query performance and reducing response times.

##### EC family

The 'EC' sub-family of VM size series are one of Azure's security focused memory-optimized VM instances. They're designed for confidential computing with enhanced data protection and integrity, featuring various hardware-based Trusted Execution Environments (TEEs). These instances are ideal for memory-intensive workloads, such as large databases, big data analytics, and enterprise applications that require significant amounts of RAM to maintain high performance.

View the full EC family page

Memory-Intensive Workloads: Any workload that demands a large memory footprint to efficiently handle tasks, such as simulations, large-scale computations in scientific research, or financial risk modeling.

Large Databases and SQL Servers: They are ideal for hosting large relational databases like SQL Server and NoSQL databases that benefit from high memory capacities for improved performance in data processing and transaction handling.

Enterprise Applications: Suitable for resource-intensive enterprise applications, including large-scale ERP and CRM systems, where the availability of ample memory is crucial for managing complex transactions and user loads.

Big Data Applications: Effective for big data analytics applications that need to process vast amounts of data in memory to speed up analysis and insights generation.

In-Memory Computing: Such as in-memory databases (e.g., SAP HANA) that require large amounts of RAM to keep the entire dataset in memory, allowing for ultra-fast data processing and query responses.

Data Warehousing: Provides the necessary resources for data warehousing solutions that handle and analyze large datasets, improving query performance and reducing response times.

##### M family

The 'M' family of VM size series are one of Azure's ultra memory-optimized VM instances designed for extremely memory-intensive workloads, such as large in-memory databases, data warehousing, and high-performance computing (HPC). Equipped with substantial RAM capacities and high vCPU capabilities, the M-family VMs support applications and services that require massive amounts of memory and significant computational power. High resource allocation makes the M-family particularly well-suited for handling tasks such as heavy SQL Server and other RDBMS workloads, complex scientific simulations, real-time data processing, and large-scale enterprise resource planning (ERP) systems, ensuring peak performance for the most demanding data-centric applications.

View the full M family page

SQL Server workloads with high memory needs: The M-family is particularly effective for running SQL Server machines with high memory requirements, such as for online transaction processing (OLTP) or data analytics.

In-memory databases: The M-family is particularly effective for running in-memory databases that require large amounts of RAM like SQL Server, or SAP HANA.

Big data applications: The M-family is ideal for handling big data applications that need to process and analyze huge datasets in memory, improving performance and reducing the time to insights.

Data warehousing: M-family VMs provide the performance and memory needed for data warehousing applications, facilitating faster queries and better handling of large volumes of data.

Enterprise applications: The M-family supports large-scale enterprise applications, including ERP and CRM systems, which benefit from having more memory to manage larger datasets and more complex transactions efficiently.

Heavy workloads in virtualized environments: The M-family is well-equipped to handle heavy virtualized environments, offering substantial memory for hosting multiple virtual machines and applications on a single physical server.

### Storage optimized

Storage optimized virtual machine (VM) sizes offer high disk throughput and IO, and are ideal for Big Data, SQL, NoSQL databases, data warehousing, and large transactional databases. Examples include Cassandra, MongoDB, Cloudera, and Redis.

- 
Family list

- 
L family

List of storage optimized VM size families:

Family
Workloads
Series List

L-family
High disk throughput and IO 
 Big Data 
 SQL and NoSQL databases 
 Data warehousing 
 Large transactional databases
Lpsv5-series 
 Laosv5-series 
 Lasv5-series 
 Lsv4-series 
 Lasv4-series 
 Laosv4-series 
 Lsv3-series 
 Lasv3-series 
 End of Life L-family

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

##### L family

The 'L' family of VM size series are one of Azure's storage-optimized VM instances. They're designed for workloads that require high disk throughput and I/O, such as databases, big data applications, and data warehousing. Equipped with high disk throughput and large local disk storage capacities, L-series VMs support applications and services that benefit from low latency and high sequential read and write speeds. This makes them particularly well-suited for handling tasks like large-scale log processing, real-time big data analytics, and scenarios involving large databases that perform frequent disk operations, ensuring efficient performance for storage-heavy applications.

View the full L family page

Big Data Applications: L-family VMs are perfect for big data applications that need to process, analyze, and manipulate large datasets stored directly on local disks, benefiting from the high I/O performance.

Database Servers: L-family VMs provide the necessary local disk performance for SQL Server, MySQL, PostgreSQL, and other database servers that benefit from fast access to disk storage.

File Servers: L-family VMs can be used effectively as file servers within a network, handling large files and serving them with high throughput, especially useful in environments with large media files.

Video Editing and Rendering: The high disk throughput and capacity of L-family VMs are beneficial for video editing and rendering tasks, where large video files are frequently read and written to disk.

### GPU accelerated

GPU optimized VM sizes are specialized virtual machines available with single, multiple, or fractional GPUs. These sizes are designed for compute-intensive, graphics-intensive, and visualization workloads.

- 
Family list

- 
NC family

- 
ND family

- 
NG family

- 
NV family

List of GPU optimized VM size families:

Family
Workloads
Series List

NC-family
Compute-intensive 
 Graphics-intensive 
 Visualization
NC_RTXPRO6000BSE_v6-series 
 NCads_H100_v5-series 
 NCCads_H100_v5-series 
 NCv3-series 
 NCasT4_v3-series 
 NC_A100_v4-series

ND-family
Large memory compute-intensive 
 Large memory graphics-intensive 
 Large memory visualization
ND GB300-v6-series 
 ND GB200-v6-series 
 ND_MI300X_v5-series 
 ND-H200-v5-series 
 ND-H100-v5-series 
 NDm_A100_v4-series 
 ND_A100_v4-series

NG-family
Virtual Desktop (VDI) 
 Cloud gaming
NGads V620-series

NV-family
Virtual desktop (VDI) 
 Single-precision compute 
 Video encoding and rendering
NV-series 
 NVv3-series 
 NVv4-series 
 NVadsA10_v5-series 
 NVads V710 v5-series 
 End of Life NV-family

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

##### NC family

The 'NC' sub-family of VM size series are one of Azure's GPU-optimized VM instances. They're designed for compute-intensive workloads, such as AI and machine learning model training, high-performance computing (HPC), and graphics-intensive applications. Equipped with powerful NVIDIA GPUs, NC-series VMs offer substantial acceleration for processes that require heavy computational power, including deep learning, scientific simulations, and 3D rendering. This makes them particularly well-suited for industries such as technology research, entertainment, and engineering, where rendering and processing speed are critical to productivity and innovation.

View the full NC family page

AI and Machine Learning: NC-series VMs are ideal for training complex machine learning models and running AI applications. The NVIDIA GPUs provide significant acceleration for computations typically involved in deep learning and other intensive training tasks.

High-Performance Computing (HPC): These VMs are suitable for scientific simulations, rendering, and other HPC workloads that can be accelerated by GPUs. Fields like engineering, medical research, and financial modeling often use NC-series VMs to handle their computational needs efficiently.

Graphics Rendering: NC-series VMs are also used for graphics-intensive applications, including video editing, 3D rendering, and real-time graphics processing. They are particularly useful in industries such as game development and movie production.

Remote Visualization: For applications requiring high-end visualization capabilities, such as CAD and visual effects, NC-series VMs can provide the necessary GPU power remotely, allowing users to work on complex graphical tasks without needing powerful local hardware.

Simulation and Analysis: These VMs are also suitable for detailed simulations and analyses in areas like automotive crash testing, computational fluid dynamics, and weather modeling, where GPU capabilities can significantly speed up processing times.

##### ND family

The 'ND' family of VM size series are one of Azure's GPU-accelerated VM instances. They're designed for deep learning, AI research, and high-performance computing tasks that benefit from powerful GPU acceleration. Equipped with NVIDIA GPUs, ND-series VMs offer specialized capabilities for training and inference of complex machine learning models, facilitating faster computations and efficient handling of large datasets. This makes them particularly well-suited for academic and commercial applications in AI development and simulation, where cutting-edge GPU technology is crucial for achieving rapid and accurate results in neural network processing and other computationally intensive tasks.

View the full ND family page

AI and Deep Learning: ND-family VMs are ideal for training and deploying complex deep learning models. Equipped with powerful NVIDIA GPUs, they provide the computational power necessary for handling extensive neural network training with large datasets, significantly reducing training times.

High-Performance Computing (HPC): ND-family VMs are suitable for HPC applications that require GPU acceleration. Fields such as scientific research, engineering simulations (for example, computational fluid dynamics), and genomic processing can benefit from the high-throughput computing capabilities of ND-series VMs.

##### NG family

The 'NG' family of VM size series are one of Azure's GPU-optimized VM instances, specifically designed for cloud gaming and remote desktop applications. They harness powerful AMD Radeonâ¢ PRO GPUs to deliver high-quality, interactive gaming experiences in the cloud, optimized for rendering complex graphics and streaming high-definition video. This ensures gamers enjoy a seamless, responsive gaming environment accessible from any device. Additionally, NG-series VMs provide a high-quality, responsive remote desktop experience, making them ideal for users needing reliable, high-performance access to desktop applications from anywhere in the world.

View the full NG family page

Cloud Gaming: NG-family VMs harness powerful AMD Radeonâ¢ PRO GPUs to deliver high-quality, interactive gaming experiences in the cloud.

Remote Destkop: NG-family VMs can be used for remote desktop applications, providing users with a high-quality, responsive user experience.

##### NV family

The 'NV' family of VM size series are one of Azure's GPU-accelerated VM instances, specifically designed for graphics-intensive applications such as graphics rendering, simulation, and virtual desktops. Equipped with NVIDIA or AMD GPUs, NV-series VMs provide a robust platform for rendering and processing graphics-heavy tasks, making them ideal for organizations that require virtual workstations with powerful graphical capabilities. These VMs support scenarios where remote visualization, real-time collaboration, and 3D visualization are necessary, allowing users to efficiently run graphic-intensive applications directly from Azure's cloud environment.

View the full NV family page

Virtual Desktop Infrastructure (VDI): NV-family VMs are well-suited for virtual desktops that require GPU capabilities for tasks such as graphic design, video editing, and CAD applications. They provide the graphical performance necessary for smooth operation in remote desktop scenarios.

3D Visualization: NV-family VMs are ideal for running 3D applications that demand high-performance rendering, such as architectural visualizations, medical imaging, and other professional-grade graphics tasks.

Remote Graphics Work: NV-series VMs are beneficial for industries that rely on graphics-intensive software, allowing professionals to access and use applications like Adobe Photoshop, Autodesk AutoCAD, or Dassault SOLIDWORKS remotely with near-native performance.

High-Resolution Image Processing: NV-series VMs are ideal for handling extremely large vRAM applications such as high-resolution image processing and analysis. This includes tasks in fields like geospatial analysis, satellite image processing, and professional photo editing, where handling massive image files and performing complex manipulations in real-time are crucial for productivity and performance.

Video Streaming: NV-family VMs are suitable for streaming high-resolution video content, including training videos and virtual events, ensuring high-quality delivery without local hardware constraints.

### FPGA accelerated

FPGA optimized VM sizes are specialized virtual machines available with single or multiple FPGAs. These sizes are designed for compute-intensive workloads. This article provides information about the number and type of FPGAs, vCPUs, data disks, and NICs. Storage throughput and network bandwidth are also included for each size in this grouping.

- 
Family list

- 
NP family

List of field programmable gate array accelerated VM size families:

Family
Workloads
Series List

NP-family
Machine learning inference 
 Video transcoding 
 Database search and analytics
NP-series

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

##### NP family

The 'NP' subfamily of VM size series are Azure's FPGA-accelerated VM instances. They're designed for custom hardware acceleration scenarios, including machine learning inference, video transcoding, and database search & analytics. NP-series VMs are powered by AMD Xilinx Alveo U250 FPGAs and Intel Xeon 8171M (Skylake) CPUs.

View the full NP family page

Real-Time Data Processing: NP-family VMs excel in environments where data needs to be processed in real time with minimal latency, such as in financial trading, real-time analytics, and network data processing.

Custom AI and Machine Learning: NP-family VMs are suitable for accelerating AI and machine learning inference tasks, where the FPGA can be programmed to execute specific algorithms sometimes faster than typical CPU or GPU-based solutions.

Genomics and Life Sciences: NP-family VMs can significantly speed up genomic sequencing tasks and other life sciences applications that benefit from custom hardware acceleration.

Video Transcoding and Streaming: FPGAs can be used to accelerate video processing tasks such as transcoding and real-time video streaming, optimizing performance and reducing processing times.

Signal Processing: NP-family VMs are ideal for applications in telecommunications and signal processing where rapid manipulation and analysis of signals are necessary.

Database Acceleration: NP-family VMs can enhance database operations, especially for custom search operations and large-scale database queries, by offloading these tasks to the FPGA.

### High performance compute

Azure High Performance Compute VMs are optimized for various HPC workloads such as computational fluid dynamics, finite element analysis, frontend and backend EDA, rendering, molecular dynamics, computational geoscience, weather simulation, and financial risk analysis.

- 
Family list

- 
HB family

- 
HC family

- 
HX family

List of high performance computing optimized VM size families:

Family
Workloads
Series List

HB-family
High memory bandwidth 
 Fluid Dynamics 
 Weather modeling
HBv2-series 
 HBv3-series 
 HBv4-series 
 HBv5-series

HC-family
High density compute 
 Finite element analysis 
 Molecular dynamics 
 Computational chemistry
HC-series (retiring May 31, 2027)

HX-family
Large memory capacity 
 Electronic Design Automation (EDA)
HX-series

To learn more about a specific size family or series, select the tab for that family and scroll to find your desired size series.

Note

HC-series (Standard_HC44rs, Standard_HC44-16rs, Standard_HC44-32rs) will be retired on May 31, 2027. After this date, remaining HC-series VMs will be deallocated, stop running, and will no longer have SLA or support. Sales of 1-year and 3-year Reserved Instances for HC-series ended on April 2, 2026. For new deployments, consider HBv5-series for higher performance and price-performance, or HX-series for high-memory HPC workloads.

The 'HB' subfamily of VM size series are one of Azure's high-performance computing (HPC) optimized H-family VM instances. They're designed for compute-intensive workloads, such as computational fluid dynamics, finite element analysis, and large-scale scientific simulations. High-performance AMD EPYC processors and fast memory on HB-series VMs offer exceptional CPU and memory bandwidth, making them ideal for applications that require extensive computational resources to perform large-scale calculations and data processing. This feature makes them well suited for industries such as engineering, scientific research, and data analysis. In these fields, fast and accurate processing is essential for productivity and new ideas.

View the full 'HB' family page

Computational Fluid Dynamics (CFD): HB-family VMs are ideal for simulations in fields like aerospace, automotive design, and manufacturing, where fluid dynamics calculations are intensive.

Finite Element Analysis (FEA): HB-family VMs are suitable for engineering analyses that simulate physical phenomena, requiring intensive computational power to model complex systems and materials.

Weather Forecasting: HB-family VMs can handle the massive datasets and complex simulations required for high-resolution weather modeling and forecasting.

Seismic Processing: Used in the oil and gas industry, HB-family VMs can process seismic data to help map and understand subsurface structures.

Scientific Research: HB-family VMs support a wide range of scientific research that requires large-scale mathematical modeling, including physics and computational chemistry simulations.

Genomics and Bioinformatics: HB-family VMs are also used in life sciences for genomic analysis, where large amounts of data need to be processed quickly to decode genetic information.

The 'HC' family of VM size series are one of Azure's high-performance computing (HPC) optimized VM instances. They're designed for compute-intensive workloads that require substantial CPU power, such as genomic sequencing, engineering simulations, and financial modeling. High-performance Intel Xeon Scalable processors and fast memory on HC-series VMs offer exceptional computational capabilities and memory bandwidth, making them ideal for applications that demand intense processing power to handle complex calculations and massive data sets efficiently. These VMs are designed for sectors like healthcare, finance, and engineering, where rapid data processing and simulation accuracy are critical for advanced research and development.

View the full HC family page

Genomic Sequencing: HC-series VMs provide the computational power needed for genomic sequencing, enabling researchers to process and analyze large genetic datasets quickly.

Engineering Simulations: Ideal for running complex simulations in fields such as automotive, aerospace, and mechanical engineering. These simulations often include finite element analysis (FEA) and computational fluid dynamics (CFD).

Financial Modeling: These VMs can handle the high demands of financial applications, including risk analysis and quantitative simulations, which require massive computational resources to execute many calculations quickly.

Scientific Research: HC-series VMs support a wide range of scientific computing needs, particularly in physics and chemistry, where large-scale computations and data analysis are crucial.

Weather Forecasting and Climate Simulation: They're used in meteorology for high-resolution weather modeling and climate simulations, which require processing large datasets and performing complex simulations.

Note

Sales of 1-year and 3-year Reserved Instances for HC-series ended on April 2, 2026. HC-series is scheduled for retirement on May 31, 2027. Plan capacity accordingly.

The 'HX' family of VM size series are one of Azure's high-memory, high-performance computing (HPC) optimized VM instances. They're designed for memory-intensive workloads that require both large amounts of RAM and significant CPU performance, such as in-memory databases, big data analytics, and complex scientific simulations. Expansive memory and powerful CPUs on HX-series VMs provide the necessary resources to efficiently handle large datasets and perform rapid data processing. These VMs are designed for sectors like financial services, scientific research, and enterprise resource planning, where managing and analyzing large volumes of data in real-time is crucial for operational success and innovation.

View the full HX family page

In-Memory Databases: HX-series VMs are excellent for hosting in-memory databases, which require extensive memory to maintain large datasets in RAM for ultra-fast processing and access.

Big Data Analytics: They can handle big data analytics applications that need to process vast amounts of data in memory to speed up analysis, which is critical for real-time decision-making.

Genomic Research: Genomics research often involves large-scale data analysis, where high memory capacity can significantly enhance performance by allowing more of the dataset to be held in memory, speeding up the analysis.

Financial Simulations: Financial institutions use HX-series VMs for high-frequency trading platforms and risk management simulations that require rapid processing of large data volumes to predict stock trends or calculate credit risks in real time.

ERP Systems: Large enterprise resource planning (ERP) systems benefit from the high memory and processing power of HX-series VMs to manage and process extensive enterprise data and support large numbers of concurrent users effectively.

### List available machine sizes by region.

The Azure CLI can be leveraged to identify which machine sizes are available for a particular region using the command:

`az vm list-skus --location <region> --output table
`

## Learn platform sizes content

- For information about pricing of the various sizes, see the pricing pages for Linux or Windows.

- Want to change the size of your VM? See Change the size of a VM.

- For availability of VM sizes in Azure regions, see Products available by region.

- To see general limits on Azure VMs, see Azure subscription and service limits, quotas, and constraints.

- For more information on how Azure names its VMs, see Azure virtual machine sizes naming conventions.

## REST API

For information on using the REST API to query for VM sizes, see the following:

- List available virtual machine sizes for resizing

- List available virtual machine sizes for a subscription

- List available virtual machine sizes in an availability set

## Benchmark scores

Learn more about compute performance for Linux VMs using the CoreMark benchmark scores.

Learn more about compute performance for Windows VMs using the SPECInt benchmark scores.

## Other size information

List of all available sizes: Sizes

Pricing Calculator: Pricing Calculator

Information on Disk Types: Disk Types

## Next steps

Take advantage of the latest performance and features available for your workloads by changing the size of a virtual machine.

Utilize Microsoft's in-house designed ARM processors with Azure Cobalt VMs.

Learn how to Monitor Azure virtual machines.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
