---
layout: post
title: How to Mount Azure Storage to Azure Databricks
categories: how2
comments: true
---

## Introduction
I found multiple articles on how to mount an Azure Storage account in Azure Databricks, but most of them refered to using the Azure Key Vault which I do not want to setup at this time. So I decided to continue my quest as I required the storage account and container to be mounted for me to read the *.sas7dbat files into a Dataframe. I also could not find clear instructions on how to use the Databricks CLI in Azure Databricks.

## Prerequisites
 1. [Azure Subscription](https://azure.microsoft.com/en-us/free/)
 1. [Azure Storage Account](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal) with a [Container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) ready
 2. [Azure Databricks](https://azure.microsoft.com/en-us/services/databricks/#:~:text=Azure%20Databricks%20provides%20the%20latest,scale%20and%20availability%20of%20Azure)

### Code

First we will need to generate a SAS Token, which we can achieve by following this guide by June Castillote [here](https://adamtheautomator.com/azure-sas-token/).

I prefer to create a [new Scala Notebook](https://docs.databricks.com/notebooks/index.html) for the next part, so that I can save it and remember how I achieved this in the future. With the below script we start off by creating all the required variables for the actual mounting function. For a more complete guide see below link in the External Links for the full article by Gauri Mahajan

```scala
val containerName = "<Enter Container Name Here>"
val storageAccountName = "<Enter Storage Account Here>"
val sas = "<Enter SAS Key Here>"
val config = "fs.azure.sas." + containerName+ "." + storageAccountName + ".blob.core.windows.net"
```

Once all the parameters is set, we can go ahead and mount the storage container into Azure Databricks. Remeber to change the mount name in the below script.

```scala
dbutils.fs.mount(
  source = "wasbs://" + containerName + "@" + storageAccountName + ".blob.core.windows.net/",
  mountPoint = "/mnt/<Enter Unique Mount Name Here>/",
  extraConfigs = Map(config -> sas))
```

## Data Exploration

Once we have our Storage Account mounted, we can start exploring the data in these mounts. First off lets look at all of our mapped mounts.

```scala
display(dbutils.fs.mounts())
```

If you want to have a look at what files are in our Storage Account, you can use the below script.

```scala
dbutils.fs.ls("/mnt/<Enter Unique Mount Name Here>")
```

![@JPVoogt](/public/img/JVoogt_Mounting-Azure-Storage-in-Azure_Databricks-Using-SAS.png){:class="img-responsive"}

And if for any reason you want to unmount the Storage Account you can use the below script.

```scala
dbutils.fs.unmount("/mnt/<Enter Unique Mount Name Here>/")
```

## External Links

[Comprehensive Guide](https://www.sqlshack.com/accessing-azure-blob-storage-from-azure-databricks/)

{% include post_footer.html %}
