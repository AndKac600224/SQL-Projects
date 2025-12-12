# SQL Query Performance Analysis Report

An academic report (AGH, Applied Informatics) focusing on the detailed execution analysis of SQL queries. This project demonstrates fundamental concepts of database optimization, including the critical impact of Primary Keys, logical operators, and indexes.

This report documents one of my **first practical engagements** with performance tuning in a database environment, utilizing MS SQL Server and the AdventureWorks2019 dataset.

## Project Structure

SQL projects/ 
├── Sprawozdanie-bazy_danych.pdf # The full report (in Polish) containing analysis, results, and SQL commands. 
└── README.md # This file 

## How to Explore

1. **Review the Report:** Read the `Sprawozdanie-bazy_danych.pdf` to see the full analysis, statistical data, and conclusions.
2. **Key Query:** The core of the analysis is the performance of the following query on the `Sales.SalesOrderDetail` table:
   ```sql
   SELECT SalesOrderID, SalesOrderDetailID
   FROM Sales.SalesOrderDetail
   WHERE SalesOrderID = 43683 AND SalesOrderDetailID = 240;
   ```
3. **Analyze Scenarios**: The report details the execution costs (Time, I/O, CPU) under three main scenarios: 
  * **Scenario 1**: Primary Key Impact: Comparing execution with and without the PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID constraint. 
  * **Scenario 2**: Logical Operator Impact: Comparing the original query (...WHERE...AND...) against a modified version using OR (...WHERE...OR...). 
  * **Scenario 3**: Nonclustered Index: Analyzing the impact of adding a nonclustered index on the UnitPriceDiscount column.

## Features & Key Findings

  * **Primary Key (PK) Validation**: Demonstrated that removing the clustered PK increased execution time from ~0.001s to ~0.046s and raised the number of processed rows from 1 to 121,317. This confirms the PK's role in rapid row identification.
  * **Operator Efficiency**: The logical operator AND proved to be more efficient than OR in terms of cost and time, as it drastically reduces the required result set, requiring less system overhead.
  * **Execution Plan Analysis**: Utilized the Include Actual Execution Plan tool in MS SQL Server to gather detailed statistics on I/O cost, CPU cost, and processing time.
  * **Index Optimization Note**: The final experiment noted that the database system automatically selected the most optimal index (clustered PK) even after a nonclustered index was added, making a direct comparison of index types challenging in the given environment.

## Technologies & Concepts
 * SQL (T-SQL)
 * MS SQL Server
 * AdventureWorks2019 Database
 * Database Indexing: Clustered vs. Nonclustered Indexes
 * Primary Keys and Constraints
 * Query Optimization and Execution Plans
 * Logical Operators (AND, OR)
