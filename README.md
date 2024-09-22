# sql-learnings

Viewing query plans on multiple queries can be done using system views: eg sys.dm_exec_query_plan
![image](https://github.com/user-attachments/assets/1ed3b5c7-04f9-4076-bce9-3bc6bc22694f)

Execution plan: estimated vs actual:
![image](https://github.com/user-attachments/assets/83bcffa5-8498-4d40-a88b-145f8b7e3051)

fat arrows means more data is passed
(dotted lines means it's still executing this phase)
**1st operator** is most important to check (rightmost one)
You can **compare** 2 execution plans: save one execution plan (right click) and compare (also right click)

**Query plan cache and reuse:**
hard coded values are part of the query => query plan cannot be reused, so avoid adhoc queries: parameterize to allow reuse: 
EXEC sp_executeSql mysqlstatement @paramsDef @param1=value @param2=value ...
*or use setting "optimize for ad hoc workload" (no downsides)
using stored procedures has the same advangtage

sys.dm_exec_cached_plans 

**indexing**
goal is to have as** few indexes** as possible to improve as many queries as possible

rowstore(for OLTP, transactional)  vs columnstore (for OLAP, analytic workloads), clustered vs non clustered indexes

to see what is going on:
set statistics **IO, time** ON

**statistics** 
- used for where and order by, not for select
- created automatically for your indexes
- 
