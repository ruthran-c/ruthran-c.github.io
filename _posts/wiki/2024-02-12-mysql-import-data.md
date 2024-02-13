---
title: Faster import of data into MySQL
date: 2024-02-12 23:35:00 -0500
categories: [Wiki]
tags: [mysql, sql, workbench, homebrew, pics]
pin: true
---

Importing data from a `.csv` file into a MySQL database using Workbench's data import wizard is 
notoriously slow. My recent import of a `(500000, 6)` shaped table into MySQL using the wizard took over an hour's
time.[^workbench]

> One more reason for more people to prefer loading and analysing data using **Pandas**.
{: .prompt-info}

## Objective
To load data from a local `.csv` file into MySQL through `LOAD DATA INFILE`.

## Prerequisites
1. [MySQL installed](https://formulae.brew.sh/formula/mysql) - I did it through `homebrew`.
2. [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) 
(Optional) - SQL Client & Visual tool for databases.

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
![Workbench option](wiki/20240212-workbench.png){: w="500" h="250"}

## LOAD DATA INFILE
```sql
-- In SQL Workbench or command line (mysql> ...).
load data local infile '~/path/to/file.csv'
into table database_table
fields terminated by ','
enclosed by '"'
lines terminated by '\n'
ignore 1 rows;
```
## Error: file request rejected/ loading local data disabled 
> If the `local_infile` option is not enabled in both the client and server sides, 
> we'll encounter an ERROR 2068 or 3950 with an import fail.
{: .prompt-warning}

This variable controls server-side LOCAL capability for `LOAD DATA` statements. 

In our case the client (Workbench) and the server (MySQL Server) coexists on the same machine.
So we can edit the existing MySQL connection in Workbench to allow LOCAL capability.[^error2068]

1. In Workbench, go to Tools -> Database -> **Manage Connections**.
2. Right-click the connection and click '**Edit connection**'.
3. Select '**Advanced**' option. Paste `OPT_LOCAL_INFILE=1` in the '**Others**' box.
5. Click '**Test Connection**'. It will successfully update the connection.
6. Click close and restart Workbench.

> You can also do this through the command line/ terminal.[^error3950]
{: .prompt-info}
1. Exit from `mysql`.
2. Use command `mysql --local-infile=1 -u root -p` to connect to mysql.
3. `USE database`
4. `LOAD DATA INFILE ...;`

| | |
|----------------------------------------------------|-----------------------------------|
|![edit connections](wiki/20240212-connections.png) | ![add OPT_LOCAL_INFILE](wiki/20240212-infile.png)|

## Final Thoughts
And voilà, this method of loading data to a table is superfast in mysql. 
With very large sets, we might want to break up this `LOAD DATA INFILE` import into manageable, 
reasonably sized chunks.[^speed]

We can also accomplish the above using `mysqlimport`. It's a command line interface for 
MySQL's `LOAD DATA INFILE` statement.[^mysqlimport].

The wiki on how to use `mysqlimport` will be refined and updated at a later date 
after I've gained practical experience with it.

Thanks for reading! Hope this helps.

## Resources
[^workbench]: [MySQL Workbench - Table Data Export and Import Wizard.](https://dev.mysql.com/doc/workbench/en/wb-admin-export-import-table.html)
[^mysqlimport]: [mysqlimport — A Data Import Program.](https://dev.mysql.com/doc/refman/8.0/en/mysqlimport.html)
[^error2068]: [Error code 2068: file requested rejected due to restrictions on access with root user.](https://stackoverflow.com/questions/63264360/error-code-2068-file-requested-rejected-due-to-restrictions-on-access-with-root)
[^error3950]: [ERROR: Loading local data is disabled - this must be enabled on both the client and server sides.](https://stackoverflow.com/questions/59993844/error-loading-local-data-is-disabled-this-must-be-enabled-on-both-the-client)
[^speed]:[mysqlimport speed.](https://stackoverflow.com/questions/51901271/mysqlimport-speed-tab-delimited-dump-files-vs-sql-format-files)