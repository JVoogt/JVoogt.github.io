---
layout: post
title: Create SQL Code Snippets in Azure Data Studio
categories: how2
comments: true
---

## Introduction

I recently decided to make to move from SSMS to Azure Data Studio due to the fun additional features is brings to the table. I enjoy Visual Studio Code and, my understanding is that Azure Data Studio is built on the same codebase. It is the small things that hooked me like Zen Mode, Source Control Integration and then Notebooks of coarse. I will be writing a post on Notebooks soon.

So today I want to show you how to add your own code snippets. I use INFORMATION_SCHEMA quite often to find a tables or a columns in our databases. So this is what code snippet we will be creating today.

## Prerequisites

 1. Have [Azure Data Studio](https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver15) Installed

## Creating our first Snippet

 1. Open Azure Data Studio :)
 2. Press "CTRL + SHIFT + P" to open the Command Pallet
 3. Type "User Snippets" into the Command Pallet and Press "ENTER"
 4. Now type "SQL" and Press "ENTER"
 5. This will open "sql.json" file and this is where you will add the code below

    ```json
        "Find Object": {
            "prefix": "sqlInfo",
            "body": [
                "SELECT * FROM INFORMATION_SCHEMA.${1|COLUMN,TABLE|}S WHERE ${1|COLUMN,TABLE|}_NAME LIKE '%${2:Search}%'"
            ],
            "description": "Find Object Information"
        }
    ```

 6. Save the "sql.json" file and close it
 7. Now we finally get to use our newly created code snippet, Open a empty sql script
 8. Type in the prefix we define above "sqlInfo" and press tab
 9. Now select Table/Column as per the list we defined in our code above, Select what you are looking for and press "TAB" and press "TAB" again to move to the search criteria.
 10. Type the Table or Column Name you are looking for, then press "TAB" again to move out of the snippet context.

<iframe width="420" height="315" src="https://youtu.be/4Bd2Ibb3wyY" frameborder="0" allowfullscreen></iframe>

## External Links

[Offical MS Docs for Snippets](https://docs.microsoft.com/en-us/sql/azure-data-studio/code-snippets?view=sql-server-ver15)

{% include post_footer.html %}
