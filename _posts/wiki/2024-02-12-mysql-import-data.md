---
title: Faster import of data into MySQL
date: 2024-02-12 23:35:00 -0500
categories: [Wiki]
tags: [mysql, sql, workbench, homebrew]
---

Importing data from a `.csv` file into a MySQL database using Workbench's data import wizard is 
notoriously slow. My recent import of a `(500000, 6)` shaped table into MySQL using the wizard took over an hour's
time.[^workbench]

> One more reason for more people to prefer loading and analysing data using **Pandas**.
{: .prompt-info}

## Objective
To load data from a local `.csv` file into MySQL through `LOAD DATA INFILE`.

## Prerequisites
1. MySQL installed - I did it through `homebrew`.
2. MySQL Workbench (Optional) - Visual tool for databases.

## Steps
### Create table to import data
Firstly, we need a table in MySQL for the data to be imported into. If the table already exists, all fine.
Else, we need to create a new table in MySQL either through the command line or through MySQL Workbench.

> My shortcut 👉 Use Workbench's data import wizard to start the process of importing 
> the `.csv` file, cancel the process right after and purge the imported rows. This leaves us with a nice
> parametrised empty table to fast import later.
{: .prompt-tip}

To do this,
1. In MySQL Workbench, right-click on the database (schema) into which you want the table added.
2. Click on `Table Data Import Wizard`
3. The wizard will take you through the steps to import data.
4. In the final page of the wizard, you'll be able to see the log for the import. Once the log is active,
and you see multiple lines of `- Data import`, we're good to go.
5. Cancel the process and refresh the schemas using the 🔄 button. You should see the new table appear.
6. Right-click on the table and hit `Truncate Table`.

We now have a proper empty table for data imports!

![Workbench option](/assets/img/20240212-workbench.png)


## Resources
[^workbench]: [MySQL Workbench - Table Data Export and Import Wizard](https://dev.mysql.com/doc/workbench/en/wb-admin-export-import-table.html)
