---
layout: post
title: Read and Write Data From Azure Synapse to Azure Databricks
categories: code
comments: true
---

## Introduction

Working with big datasets has introduced many more technologies for the average Data Analyst to learn and understand. I have recently started to work more in Azure Databricks to enable our processes to be considered more optimized. For example, I do a lot of string distance calculations on my datasets and, SQL Server or even Azure Synapse is not always the best solution for this. In the past, we created these functions as CLR's and processed the data directly in SQL, but in time our data grew even more and, this became harder and harder. Moving this workload to Azure Databrick saved us hours of processing time, but introduced a new technology barrier that we had to learn and overcome.

Below I go through the basic outline of what is required to load data from Azure Synapse to Azure Databricks and push down to Synapse again once done.

 1. Configure your BLOB storage access, this can be achieved in many other ways. Read more [here](https://docs.databricks.com/data/data-sources/azure/azure-storage.html)
 2. Create the JDBC connection string and BLOB connection string
 3. Read the data from Azure Synapse into a Spark Dataframe using [spark.read](https://spark.apache.org/docs/latest/sql-data-sources-load-save-functions.html) function
 4. Write transformed data back into Azure Synapse with [spark.write](https://spark.apache.org/docs/2.3.0/sql-programming-guide.html)


 ![@JPVoogt](/public/img/JVoogt_Read-and-Write-Data-From-Azure-Synapse-to-Azure-Databricks_1.png){:class="img-responsive"}


## Code

#### CONFIGURE BLOB CREDENTIALS

{% highlight python %}
spark.conf.set( "fs.azure.account.key.<>.blob.core.windows.net", "")
{% endhighlight %}

#### CONFIGURE JDBC AND BLOB PATH

{% highlight python %}
jdbc = "jdbc:sqlserver://<SERVERNAME>.database.windows.net:1433;database=;user=@;password=;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;" 
blob = "wasbs://@.blob.core.windows.net/"
{% endhighlight %}

#### READ DATA FROM SYNAPSE INTO DATAFRAME

{% highlight python %}
df = spark.read
.format("com.databricks.spark.sqldw")
.option("url", jdbc)
.option("tempDir", blob)
.option("forwardSparkAzureStorageCredentials", "true")
.option("Query", "SELECT TOP 1000 * FROM <> ORDER BY NEWID()")
.load()
{% endhighlight %}

#### WRITE DATA FROM DATAFRAME BACK TO AZURE SYNAPSE

{% highlight python %}
df.write
.format("com.databricks.spark.sqldw")
.option("url", jdbc)
.option("forwardSparkAzureStorageCredentials", "true")
.option("dbTable", "YOURTABLENAME")
.option("tempDir", blob)
.mode("overwrite")
.save()
{% endhighlight %}


{% include post_footer.html %}
