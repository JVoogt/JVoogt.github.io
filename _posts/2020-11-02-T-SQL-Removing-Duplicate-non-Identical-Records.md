---
layout: post
title: T-SQL Removing Duplicate non-Identical Records
categories: code
comments: true
---

## Introduction

I found that some of us repeat the same processes over and over again where other people might never need to perform a specified task which I would consider basic, thus I want to share with you how I approach removing of duplicate records in my data. Now if you are lucky enough that the entire row is a complete duplicate then you can just go ahead and slap a **DISTINCT** in your query and your problem should be gone. You will have to be mindful of the limitations here as it doesn't support long text fields as per [Microsoft Docs](https://docs.microsoft.com/en-us/sql/odbc/microsoft/distinct-keyword-limitations?view=sql-server-ver15)

I Prefer to rather decide what makes my records distinct and act accordingly.

## Remove Duplicate Records for Reporting

#### Description 

When removing duplicates you will have to decide what makes your record unique, could it be a merchant id or even a social security number? I Like to go with the [CTE](https://docs.microsoft.com/en-us/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-ver15) and [ROW_NUMBER](https://docs.microsoft.com/en-us/sql/t-sql/functions/row-number-transact-sql?view=sql-server-ver15) approach when removing duplicates from me datasets. The only drawback here is, if you do not want the new column you will have to specify the required columns when you select from the [CTE](https://docs.microsoft.com/en-us/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-ver15)

#### Code

{% highlight sql %}
WITH CTE
AS
(
    SELECT  *
            , ROW_NUMBER() OVER(PARTITION BY [<WHAT COLUMN/S MAKE MY RECORD UNIQUE>] ORDER BY [<YOUR PREFERED ORDER>]) RN
    FROM    [myTable]
)
SELECT  *
FROM    CTE
WHERE   RN = 1
{% endhighlight %}


## Remove Duplicate Records From Table

#### Description 

Sometimes you are not just removing duplicates for reporting purposes and you want to delete the duplicates from the actual table. SQL Server allows this awesome trick where you can write your logic in a [CTE](https://docs.microsoft.com/en-us/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-ver15) and then [DELETE](https://docs.microsoft.com/en-us/sql/t-sql/statements/delete-transact-sql?view=sql-server-ver15) records based on the [CTE](https://docs.microsoft.com/en-us/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-ver15) logic as per the below example. Here I delete all records that occurred more than once.

#### Code

{% highlight sql %}
WITH CTE
AS
(
    SELECT  *
            , ROW_NUMBER() OVER(PARTITION BY [<WHAT COLUMN/S MAKE MY RECORD UNIQUE>] ORDER BY [<YOUR PREFERED ORDER>]) RN
    FROM    [myTable]
)
DELETE FROM CTE
WHERE   RN != 1
{% endhighlight %}



{% include post_footer.html %}
