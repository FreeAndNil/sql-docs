---
description: "sp_query_store_reset_exec_stats (Transact-SQL)"
title: "sp_query_store_reset_exec_stats (Transact-SQL)"
ms.custom:
- event-tier1-build-2022
ms.date: "04/26/2022"
ms.prod: sql
ms.prod_service: "database-engine, sql-database"
ms.reviewer: ""
ms.technology: system-objects
ms.topic: "reference"
f1_keywords: 
  - "sp_query_store_reset_exec_stats_TSQL"
  - "sys.sp_query_store_reset_exec_stats_TSQL"
  - "sys.sp_query_store_reset_exec_stats"
  - "sp_query_store_reset_exec_stats"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_query_store_reset_exec_stats"
  - "sys.sp_query_store_reset_exec_stats"
ms.assetid: 899df1ff-e871-44df-9361-f3b87ac3ea31
author: markingmyname
ms.author: maghan
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sp_query_store_reset_exec_stats (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Clears the runtime stats for a specific query plan from the Query Store. If you [enable Query Store for secondary replicas](../performance/monitoring-performance-by-using-the-query-store.md#enable-query-store-for-secondary-replicas), `sp_query_store_reset_exec_stats` can only be executed against the primary replica. The procedure's scope applies to the entire replica set.
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
sp_query_store_reset_exec_stats [ @plan_id = ] plan_id [;]  
```  
  
## Arguments  
`[ @plan_id = ] plan_id`
 Is the id of the query plan to being cleared. *plan_id* is a **bigint**, with no default.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Permissions  
 Requires the **ALTER** permission on the database. 
  
## Examples  
 The following example returns information about the queries in the query store.  
  
```sql
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 After you identify the plan_id that you want to clear the statistics, use the following example to delete the execution stats for a specific query plan. This example deletes the execution stats for plan number 3.  
  
```sql
EXEC sp_query_store_reset_exec_stats 3;  
```  
  
## Next steps

Learn more about Query Store in the following articles:

- [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
- [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
- [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
- [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
- [sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
- [Query Store Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
- [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) 
