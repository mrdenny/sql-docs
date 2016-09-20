---
title: "Glossary (SQL Server PDW)"
ms.custom: na
ms.date: 07/27/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6cedd2e4-5101-4c9d-9fe8-fba7ee58f032
caps.latest.revision: 65
author: BarbKess
---
# Glossary (SQL Server PDW)
This is the glossary of terms for SQL Server PDW.  
  
## Terms  
  
|Term|Definition|  
|--------|--------------|  
|Admin Console|A web application that displays the appliance state information. Users can connect to the Admin Console through Windows Internet Explorer.|  
|appliance|An application architected to run on specific hardware and software that function together as one box. Users can only access the box through the user interface of the application.|  
|Appliance backup|An ***appliance backup*** is a backup of everything that is needed to restore the entire appliance. This includes a full (or full plus differential) backup of all user databases and a backup of the master database.|  
|appliance-level collation|The collation that is applied to all metadata and databases in the SQL Server PDW appliance. When a database is created, the default collation is the appliance-level collation.|  
|appliance node|A unit of hardware and software resources architected for a specific purpose. The SQL Server PDW architecture contains several types of appliance nodes.|  
|Backup server|A server that is used for backup and restore operations.  BACKUP DATABASE writes backups to the backup server. RESTORE DATABASE restores backups from the backup server.<br /><br />This server is part of your own customer network and is not shipped with the appliance. SQL Server PDW uses a Windows file share to access data on the backup server. You can use the backup server for additional purposes, depending on your business requirements.|  
|bi-level cache|A characteristic of the SQL Server PDW shared nothing architecture in which the Control node and each Compute node have separate query caches. This enables the each node to process queries locally occur without sharing the cache. The Control node query cache holds results for entire queries, whereas the Compute node query cache holds results for Compute node queries only.|  
|collation|A collation specifies the rules for how strings of character data are sorted and compared, based on the norms of a particular language and locale. For example, in an ORDER BY clause, an English speaker would expect the character string 'Chiapas' to come before 'Colima' in ascending order. However, a Spanish speaker in Mexico might expect words beginning with 'Ch' to appear at the end of a list of words starting with 'C'. Collations dictate these kinds of sorting and comparison rules. The Latin_1 General collation will sort 'Chiapas' before 'Colima' in an ORDER BY ASC clause, whereas the Traditional_Spanish collation will sort 'Chiapas' after 'Colima'.|  
|colocated data|Data that is stored and processed in the same location. In the SQL Server PDW appliance, data is colocated on each node. Colocation enables queries to run in parallel without impacting each other's performance.|  
|complex join|A join on a non-distribution key column of a distributed table. This usually requires SQL Server PDW to copy data among the Compute nodes prior to performing the join.|  
|Compute node|The basic unit of scalability for performance and storage. Each Compute node in the SQL Server PDW appliance uses its own user-data and computing resources to perform a portion of a parallel query. Because each Compute node is independent and self-sufficient, you can improve query performance on large data sets by adding more compute nodes.<br /><br />The Compute nodes are the data storage and query processing backbone of the appliance. Each Compute node stores subsets of distributed data and performs massively parallel processing (MPP) query operations. Each Compute node receives query plan operations from the Control node, runs the query plan operations (which can be data transfer operations or Transact\-SQL operations), and returns the results to the Control node.<br /><br />Each Compute node in the SQL Server PDW appliance uses its own user-data and computing resources to perform a portion of a parallel query. Because each Compute node is independent and self-sufficient, you can scale out query performance and storage capacity by adding more Compute nodes.|  
|Configuration Manager Tool|See SQL Server PDW Configuration Manager Tool.|  
|Control node|Central point of control for processing queries on the SQL Server PDW appliance. The Control node receives the user query, creates a distributed query plan, communicates relevant plan operations and data to Compute nodes, receives compute node results, performs any necessary aggregation of results, and then returns the query results to the user. This node must be available in order to run queries on the appliance.|  
|control node aggregation|Calculations performed on the Control node to aggregate the results from parallel queries. For example, the control node aggregates the results for the SUM and AVG function.|  
|control rack|The control rack houses the servers, storage, and networking components for the nodes that provide control, management, or user interface functions. The control rack is the interface between the user and the Compute nodes.|  
|control node saturation|A performance bottleneck on the Control node. A can occur when the Control node performs a large amount of aggregation.|  
|control rack|Houses the hardware that provides control, management, and user interface functions for the SQL Server PDW appliance. The control rack is the interface between the user and the Compute nodes. There is only one control rack per appliance.|  
|data distribution scheme|The strategy for storing tables across the SQL Server PDW appliance. For example, tables can be distributed (split, divided) or replicated (copied, duplicated).|  
|data mart|A collection of read-only data used for a specific business purpose. The data mart is usually populated from a larger collection of data that is stored in a data warehouse.|  
|Data Movement Service (DMS)|A SQL Server PDW service that manages communication and data transfer among the appliance nodes. This includes interfacing with the SQL Server instances in the SQL Server PDW appliance. DMS improves query performance by optimizing data transfer speeds.|  
|Data provider|A layer of software that handles communication between data extensions and customized software specific to each type of external data source. Depending on the specific data source, multiple data providers are available from Microsoft and from third-party vendors.|  
|data rack|The physical storage container for the compute node hardware. A data rack houses the servers, storage arrays, and networking components for a group of compute nodes. Each data rack within an appliance has the same number of Compute nodes; however, the number of Compute nodes in the data rack can vary among hardware vendors.<br /><br />Because the data rack has the single purpose of housing Compute nodes, when designing the SQL Server PDW appliance, you can increase the number of Compute nodes by adding data racks.|  
|data skew|A condition that occurs when the rows of a distributed table are not spread uniformly across all of the distributions. A significant variation in the number of rows in each distribution can negatively impact query performance.<br /><br />To avoid data skew, choose a distribution key column whose values have a uniform distribution. For example, a column with random numbers will have a uniform spread across the distributions. Conversely, if a distribution column has repeating values such as time, date, or product price, the values can nucleate around a specific value and cause data skew.|  
|data warehouse|A data warehouse is a collection of data that is loaded from one or more data sources and is used for performing business intelligence tasks such as reporting and data analysis. The data loading process, also called extract, transform and load (ETL), is a major component of the data warehouse.|  
|differential backup|A database backup that only includes changes made since the last full backup. A differential backup can only be performed if the last full backup was completed successfully.|  
|distributed relational database|A database that is controlled by a central database management system (DBMS) and stored as multiple collections of data that are not all attached to a common CPU. The SQL Server PDW appliance stores collections of data across multiple SQL Server database instances.|  
|distributed table|A table whose rows are dispersed across multiple storage locations, called *distributions*.|  
|distribution|The set of table rows, from one or more distributed tables, stored in the same location. SQL Server PDW uses the value in the distribution column to deterministically assign each row to a distribution.<br /><br />To improve parallel query performance, the rows that will be joined together, in queries, should be stored together in the same distributions. This avoids transferring data among the distributions before running parallel query operations.<br /><br />As part of the shared nothing SQL Server PDW architecture, each distribution is stored on its own set of disks. To accomplish this, the storage array for each Compute node is divided into disk groups (LUNs). Each distribution is stored on one LUN of one Compute node.<br /><br />In SQL Server PDW, each Compute node stores eight distributions. For example, if there are eight Compute nodes, there will be 64 distributions (8 nodes x 8 distributions/node).|  
|distribution column|The column whose values SQL Server PDW uses to assign a distributed table row to a distribution. Each distributed table has one column designated as the *distribution column*.|  
|Domain Name System (DNS)|An internet standard for translating host names to IP addresses.|  
|DNS Server|A software program that implements the DNS standard. Applications communicate with the DNS Server to translate host names into IP addresses|  
|dwloader|A command-line tool which bulk loads rows into an existing table in the appliance. When loading rows, you can add all rows to the end of the table *(append mode)*, append new rows and update existing rows *(upsert mode)*, or delete all existing rows and insert all rows into an empty table *(reload mode)*.<br /><br />**dwloader** ships with the client tools. To use dwloader, install it onto your Loading server, and then run the tool on your Loading server.|  
|explicit permission|A permission given on an object to a login or server role via the GRANT or DENY statements. This is in contrast to an implicit permission that is inherited from a server role.|  
|full database backup|A backup of an entire SQL Server PDW database. A backup of a user database includes database users, and database roles. A backup of the master database includes logins.|  
|InfiniBand|A high speed network used for private communication inside of a SQL Server PDW appliance.|  
|implicit permission|A permission given on an object to a login or server role via inheriting an explicit GRANT or DENY permission from a server role. An object can only inherit an implicit permission if it does not have an explicit permission.|  
|linear scale out|The SQL Server PDW process of adding more Compute nodes to gain a linear increase in query performance for a given dataset.|  
|Loader|The APIs that SQL Server PDW uses to load data into the appliance. **dwloader** and the Integration Services Destination Adapters both load data by calling the Loader APIs.|  
|Loading server|A server that stores data before it is loaded and provides the processing to copy data to the appliance.<br /><br />This server is part of your own customer network and is not shipped with the appliance. You can use the Loading server for additional purposes, depending on your business requirements.<br /><br />To load data, run **dwloader** command-line tool or Integration Services on the Loading server.|  
|login|A password-protected user account for SQL Server PDW.|  
|massively parallel processing (MPP)|The process of distributing the workload for a query across multiple CPUs or machines, resulting in faster performance.|  
|MPP Engine|An appliance software component that runs on the Control node and coordinates these data warehousing functions that are specific to managing the SQL Server PDW application: Creates appliance-wide parallel query plans; coordinates parallel query execution on the Compute nodes; coordinates parallel transactions; stores and coordinates appliance-wide metadata and configuration data; manages appliance and database authentication and authorization; tracks hardware and software status.|  
|MPP query plan|The "parallelized" query plan that the MPP engine creates to run a SQL user-query in parallel across the appliance nodes. The control query plan contains query operations organized into steps. The MPP Engine runs the steps sequentially. Each step can contain serial or parallel operations. All operations within a step must be completed before the MPP Engine runs the next step.|  
|MPP query plan step|A step specifies one or more operations in the MPP query plan that must be run as a unit. For example, a step can contain multiple parallel SQL Server operations that must all complete on the Compute nodes before the engine can continue to the next step.<br /><br />When specifying SQL Server operations, a step does not contain the SQL Server query plan. Instead, the step specifies the Transact\-SQL statement; each SQL Server instance creates its own symmetric multiprocessing (SMP) query plan to run the Transact\-SQL statement.|  
|multi-level query cache|A characteristic of the SQL Server PDW shared nothing architecture in which each appliance node has its own query cache. This enables each node to process queries that locally occur without sharing the cache. For example, the Control node query cache holds the aggregated results for queries, whereas the Compute node query cache holds results for Compute node queries only.|  
|parallel backup and restore|A feature of SQL Server PDW that performs parallel copies to backup a user database from the appliance nodes to the Backup server. Similarly, when data is restored in parallel from the Backup server to the appliance nodes.|  
|remote table copy|A feature of SQL Server PDW that enables Hub and Spoke scenarios by copying the results of a SQL SELECT statement to a table in an SMP SQL Server database. The remote table copy  is initiated with the CREATE REMOTE TABLE statement.<br /><br />The SMP database is in an instance of SQL Server that is running on a Windows system which is attached to the internal InfiniBand network of the SQL Server PDW appliance. The SMP database cannot reside on a server within the SQL Server PDW appliance.|  
|query parallelization|The process of splitting a SQL query into smaller "subqueries" that can be run simultaneously. Results from the subqueries are later recombined to produce a result set for the initial query.|  
|redistribution|The process of copying data across the compute nodes in the appliance so that each distribution has all the distributed table data it needs to perform a complex join. Because a complex join is on one or more non-distribution columns, each distribution might not already have the correct data to perform its portion of the distributed complex join. Redistribution temporarily stores extra copies of row data so that each distribution can perform its portion of the complex join without retrieving data from another distribution.|  
|replicated table|A table that is stored in its entirety on each compute node. Replicated tables require storage for each copy of the table, but do not need to be copied to additional Compute nodes before performing a join.|  
|Server role|A group of principals (logins and server roles). Server roles are hierarchical. Logins and server roles can be added as members of one or more server roles. Use a server role to manage security permissions on securables (databases, tables, and views) for a group of logins and other membering server roles.|  
|shared nothing (SN)|A distributed computing architecture in which each node contains its own data, CPU, and storage to function as a self-sufficient and independent unit.|  
|simple join|A join on columns of replicated tables and/or distribution columns of distributed tables. There is no need to transfer data between distributions before performing a simple join.<br /><br />In contrast, a complex join involves a non-distribution column of a distribution table. This requires copying data among the distributions before performing the join.|  
|spare / standby|A hardware component that is kept available but not in use, intended to replace an existing appliance component in the case of a hardware failure.<br /><br />There are three types of spares:<br /><br />A hot spare is a hardware component that can be activated immediately and automatically by the appliance without administrator intervention.<br /><br />A warm spare is a hardware component that requires minimal administrator intervention (such as entering commands or flipping switches) in order to become available to the appliance.<br /><br />A cold spare is a hardware component that is not available to the appliance without significant administrator intervention and may require a significant amount of time to be brought online.|  
|SQL Server|The database for managing data storage and query processing on the appliance. Each user database is distributed among multiple SQL Server database instances. Each Compute node runs an instance of SQL Server and uses it to manage user data. The Control node also runs an instance of SQL Server and uses it to manage metadata.|  
|SQL Server PDW Configuration Manager|The SQL Server PDW Configuration Manager (PDWCM) is an appliance administration tool that SQL Server PDW system administrators use to perform appliance-level operations and to change appliance-level settings. For example, use PDWCM to reset passwords, set the time zone, change IP addresses, configure SSL certificates, enable remote access through the firewall, start or stop the appliance, and set Instant File Initialization.<br /><br />Before using SQL Server PDW for the first time, use PDWCM to complete the setup process that could not be completed at the manufacturing facility due to security precautions and unknown user environment variables, such as IP addresses.|  
|Staging database|A user-created SQL Server PDW database that stores data temporarily when it is being loaded into the appliance. When loading data, SQL Server PDW first copies the data to the staging database and then copies the data from temporary tables in the staging database to permanent tables in the destination database. If a staging database is not used, SQL Server PDW creates temporary tables in the destination database and uses them to store the loaded data before it inserts the loaded data into the permanent destination tables.<br /><br />The primary benefit of a Staging database is to reduce table fragmentation. If a Staging database is not used, the data is loaded into temporary tables in the destination database. When temporary tables get created and dropped in the destination database, the pages for the temporary and permanent tables become interleaved. Over time, this causes table fragmentation and degrades performance. In contrast, a Staging database ensures that temporary tables are created and dropped in a separate file space than the permanent table.|  
|super-user|A built-in account named the “SA” account. There is one super-user account per appliance. This account has all privileges.|  
|Symmetric Multiprocessing (SMP)|A multi-processor computer architecture where identical processors share main memory. The architecture allows simultaneous processing to be distributed among the processors. In a symmetric multiprocessing (SMP) architecture, query processing occurs within one physical instance of a database. Conversely, in a massively parallel processing (MPP) architecture, query processing occurs within multiple instances of a database that each has dedicated CPU, memory, and storage.|  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../../mpp/sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
  