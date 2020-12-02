---
layout: post
title: Learning TSQL for Analytics
categories: how2
comments: true
---

## Introduction

I have been asked to design a course outline for teaching aspiring data scientists T-SQL, now for the last 5 years I have been leading a team of Data Specialists who's bread and butter is T-SQL. But not most of them did not start out as specialists, but actually were hired with little or no previous data experience. So this should be easy right, I have helped at least 10 people in the last 3 years to become proficient in T-SQL. So where do one start, well I think there is many excellent paid and free courses out there in the wild, One for instance is an excellent video series by Kendra Little which you can find [here](https://litknd.github.io/TSQLBeginners/).

But lets get back to the problem statement, how would one structure a course outline for the aspiring data scientist, who would probably spend most of their time in either R/Python or even Scala. With the expansion of Massive Parallel Processing environments like Azure Synapse, Redshift and many more for SQL or even Spark and Databricks environments for Data Analysis in Languages like R/Python or Scala. The need for super efficient code is no long that important, don't get me wrong efficiency is still important, but can be added later.

## Outline

### Tools of the Trade

We need to decide if we want to store our data in our own environment where we are in full control of security, or move the data to the cloud where we do not have to focus on infrastructure and just the data and our data pipeline. We also need to have a look at what tools we want to use for exploring our data.

1. **Cloud vs On-Premises**
	1. 	Cloud Options
		1. Creating an Azure Account and a Azure SQL Database
	1. On-Premises Options
		1. Installing SQL Server Express/Developer Edition
1. **Tools of the Trade (IDE)**
	1. SQL Server Management Studio
	1. Azure Data Studio
	1. Visual Studio Code
	1. Spark SQL in Databricks
1. **How to start writing code**
	1. Queries
	1. Notebooks

### Introduction to the basics of the T-SQL language

Starting of with the basics of the T-SQL language, how to filter the data we want to see. We will also look at the what is a database object.

1. **Database Objects**
    1. Database -> Schemas -> Tables -> Columns -> Rows -> Record
1. **Working with the data**
	1. Selecting and limiting
		1. SELECT
		1. TOP/LIMIT
	1. Filtering Data
		1. WHERE
	1. Inline Cleaning and Modifying of our dataset
		1. UDF's and BUILT-IN Functions
	1. Grouping
		1. GROUP BY
		1. Aggregations (SUM/MIN/MAX/AVG)
	1. Ordering
		1. ORDER BY

### Working with multiple datasets and changing

In this module we will be working with multiple dataset and even make changes to the data which would persists

1. **Working with multiple datasets**
	1. Joining datasets together
		1. LEFT/RIGHT/FULL JOIN
	1. SET operators
		1. UNION/INTERSECT/EXCEPT/MINUS
1. **Building basic Processes**
	1. Stored Procedures
	1. Views
1. **Data Modifications**
	1. Adding new rows
		1. INSERT
		1. IMPORT
	1. Removing rows
		1. DELETE
	1. changing records
		1. UPDATE
1. **Analytical Functions**
	1. Window Functions
	1. Pivot and Unpivot data
	1. Analytical Aggregations
	1. Common Table Expressions (CTE)

{% include post_footer.html %}
