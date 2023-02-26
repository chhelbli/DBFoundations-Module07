# Module07 Website
---
*Christoph Helbling*  
*02/25/2023*  
*IT FDN 130 A Wi 23: Foundations Of Databases & SQL Programming*  
*Assignment7*  
*[chhelbli/DBFoundations-Module07 (github.com)](https://github.com/chhelbli/DBFoundations-Module07)*  

# Assignment7_Writeup

## Introduction
This document describes the use case for SQL User Defined Functions (UDFs) and explains the differences between Scalar, Inline and Multi-Statement Functions.

## SQL User Defined Functions
SQL offers a range of built-in functions but also gives users the option to create their own functions to return single or a table of values; such customized functions are called User Defined Functions (UDFs). 
UDFs allow a body of work to be executed in SQL based on parameters as defined by the creator of the function. UDFs are useful to check constraints or do calculations on values in a table. Another benefit is that you can reuse UDFs across queries referencing the same data.

UDFs can’t execute actions that would modify the state of a database and can’t return multiple sets of results (unlike a Stored Procedure).

This is an example of a UDF built in Assignment 7:

```SQL
Create Function fProductInventoriesWithPreviousMonthCountsWithKPIs
(@CountVsPreviousCountKPI int)
Returns Table 
 AS 
   Return( 
   Select top 1000000000 
	ProductName
	, InventoryDate
	,[Count]
	,PreviousMonthCount
	,CountVsPreviousCountKPI 
    From vProductInventoriesWithPreviousMonthCountsWithKPIs
	Where CountVsPreviousCountKPI = @CountVsPreviousCountKPI
	Order by ProductName, month(InventoryDate)
   );
Go
```

## Differences between Scalar, Inline and Multi-Statement Functions
A **Scalar Function** returns a single value. An **Inline Function** returns the output of a single select statement and does not include a BEGIN/END block. A **Multi-Statement Function** does have a BEGIN/END block and can contain several SQL statements that jointly return a single value in case of a multi-statement *scalar* function or a table of values in case of a multi-statement *table* function.

## Summary
User Defined Functions (UDFs) - in the form of scalar, inline and multi-statement functions – return a single value or a table of values based on parameters defined by the creator of the function.
