{
    "metadata": {
        "kernelspec": {
            "name": "SQL",
            "display_name": "SQL",
            "language": "sql"
        },
        "language_info": {
            "name": "sql",
            "version": ""
        }
    },
    "nbformat_minor": 2,
    "nbformat": 4,
    "cells": [
        {
            "cell_type": "markdown",
            "source": [
                "ctrl shift c ctrl shift t ctrl shift r"
            ],
            "metadata": {
                "azdata_cell_guid": "cd6c4bc8-29cb-4e36-8f3e-80c21f842366"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "### Common definitions\n",
                "\n",
                "1. Views - a stored query definition that can be used to simplify writing T-SQL statements or to secure data access, can be thought of as simplified data design to perform queries faster\n",
                "2. Stored Procedures - stored script that can include queries, DDL to create or modify objects and programming logic. they can return tabular data.\n",
                "3. User defined functions - similar to stored procedures but can return tabular data as well as single value, cant affect anything outside the function.\n",
                "4. Indexes - data structure that increases the speed of queries\n",
                "5. Constraints - rules that govern the behavious and permissible values of the table and the columns\n",
                "6. Triggers - special type of stored procedures that fires when something happens in the database like when a row is inserted or when an object is created\n",
                "7. Sequences - User defined object that generates a sequence of numbers \n",
                "8. Assemblies - references to database objects created in a .Net language, this functionality is valled common language runtime (CLR) integration"
            ],
            "metadata": {
                "azdata_cell_guid": "a13791f3-b148-4418-92ef-c1f4e5845e50"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "### SQL server files\n",
                "\n",
                "- a database must have 2 files \n",
                "\n",
                "1. data file with .mdf extension\n",
                "2. log file with .ldf extension\n",
                "\n",
                "- additional data files if used have the .ndf extension\n",
                "- data files can be grouped together strategically to backup only portions of the database\n",
                "- log file stored transactions or changes to the data to ensure consistency\n",
                "- backups of the log files can be taken for DB restoration"
            ],
            "metadata": {
                "azdata_cell_guid": "35219a4f-0d4f-4e45-82e3-9efd02f29bfa"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "### some notes\n",
                "\n",
                "- each table in a normalized database should hold information about only one type of entity and a primary key.\n",
                "- each column has a definition specifying a data type along with rules AKA constraints.\n",
                "- we can have a computed data type where the value of the column is calculated with a formula \n",
                "    - ![](data:image/png;base64,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)\n",
                "- we can have user defined data types as well\n",
                "    - like a phone number in the adventure works DB\n",
                "- we can create custom data types called CLR data types with multiple properties and methods using a .NET language such as C#"
            ],
            "metadata": {
                "azdata_cell_guid": "ca52a5dc-99ec-4d51-894f-5ab43da47f6e"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "### Indexes\n",
                "\n",
                "- everytime we create a key or a unique column we place an index on the column\n",
                "- indexes are stored separately from the data but accessed automatically when we run a query\n",
                "- and are updated everytime a row is added or removed from the table\n",
                "- index is a data structure to help DB look up information fast, usually a balanced tree on data that can be ordered and searched using the equality operators \\<,\\>,\\<=,\\>=,==, and between\n",
                "- its created automatically but we can create it with create index command\n",
                "- instead of Btrees there are other generalized types of indexes as well\n",
                "\n",
                "kinds of indexes\n",
                "\n",
                "1. clustered\n",
                "2. stores and organizes the table\n",
                "3. arrange the data in the table like sort to make look up faster\n",
                "4. a table can have only one clustered index thats because its just the entire table sorted on the cluster key\n",
                "5. when we add new rows old rows dont have to move for them to stay in order because the new row will be added into the correct data page which will have some free space\n",
                "6. a list of pointers is maintained to keep track of the order of the pages, so the rows in the other pages wont have to move\n",
                "7. usually the primary key is used as the cluster key\n",
                "8. non-clustered\n",
                "9. defined on one or more columns of the table, its a separate strcuture that points to the actual table\n",
                "10. stores the data and records in different tablesso that scanning records is faster to look for the data you want\n",
                "11. we can have 999 unclustered index per table\n",
                "12. these may be actually used if working with sparse columns\n",
                "\n",
                "indexes are optional but greatly improve performance when properly designed and implemented\n",
                "\n",
                "but they can also take up disk space\n",
                "\n",
                "If a table has four nonclustered indexes, every write to that table may require four additional writes to keep the indexes up to date\n",
                "\n",
                "### Example\n",
                "\n",
                "- phone directory, primary key is the phone number but the cluster key is the first name plus the last name\n",
                "- if the name starts with d you start looking in the beginning of the directory in your brain you did this calculation\n",
                "    - mid alphabet is j or k and d\\<j or k so it must be in the first half, thats basically a binary search\n",
                "\n",
                "### schemas\n",
                "\n",
                "- a collection to organize database objects and tables within the database\n",
                "- a User has a default schema and when accessing an object in the default schema you dont have to specify the schema name but tis good practice to do so\n",
                "- if a user has permission to create new objects the objects belong to the user's default schema unless specified other wise"
            ],
            "metadata": {
                "azdata_cell_guid": "47b25e68-9a94-4896-b3d8-c40a3fcb0692"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "### Select queries\n",
                "\n",
                "- In a select statement from is the first clause the database engine evaluates\n",
                "- The word GO doesn’t really do anything except divide the code up into separate distinct code batches."
            ],
            "metadata": {
                "azdata_cell_guid": "5757bfff-74f4-4899-94c9-95cf575910a7"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "USE AdventureWorks2022;\r\n",
                "--changing to the example database\r\n",
                "GO\r\n",
                "SELECT BusinessEntityID, JobTitle\r\n",
                "FROM HumanResources.Employee;"
            ],
            "metadata": {
                "azdata_cell_guid": "8c3bc9de-4e83-4b3d-b07b-b7b7e905ba9c",
                "language": "sql"
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                "- Column and table names need to follow specific naming rules so that SQL Server’s parser can recognize them. When a table, column, or database has a name that doesn’t follow those rules, you can still use that name, but you must enclose it within square brackets (\\[\\]).\n",
                "- SQL Server allows you to create or rename a column within a query by using what is known as an alias. You use the keyword AS to specify an alias for the column.\n",
                "- You can specify an alias name immediately following a column name. If an alias contains a space or is a reserved word—basically, keywords used to write T-SQL statements—you can surround the alias with square brackets, single quotes, or double quotes."
            ],
            "metadata": {
                "azdata_cell_guid": "e98d100c-cc53-424d-ac1f-9e7d9f7dc6ea"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT 'A Literal Value' AS \"Literal Value\",\r\n",
                "BusinessEntityID AS EmployeeID,\r\n",
                "LoginID,\r\n",
                "JobTitle\r\n",
                "FROM HumanResources.Employee;"
            ],
            "metadata": {
                "azdata_cell_guid": "4ab79e4f-73b5-42fd-94b7-b05ae8c1a7b3",
                "language": "sql",
                "tags": []
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT EMP.JobTitle\r\n",
                "FROM HumanResources.Employee AS EMP;"
            ],
            "metadata": {
                "azdata_cell_guid": "d128ab34-5a20-42aa-be5e-0a4b8587b70d",
                "language": "sql"
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                "There is a property called collation that determines whether or not case matters. If the database is set to use a case-sensitive collation, then the names of the tables and columns must match exactly.  \n",
                "  \n",
                "\n",
                "single quotes are used for literal values\n",
                "\n",
                "double quotes for column names, aliases and table names and aliases. double quotes or square brackets are necessary when name contains a space or is a keyword"
            ],
            "metadata": {
                "azdata_cell_guid": "0605b284-f488-4fac-b11c-287918e677da"
            },
            "attachments": {}
        },
        {
            "cell_type": "markdown",
            "source": [
                "1. <span style=\"color: var(--vscode-foreground);\">Switch to the AdventureWorks database&nbsp;</span> <span style=\"color: var(--vscode-foreground);\">Write a SELECT statement that lists the customers. Include the CustomerID, StoreID, and AccountNumber columns from the Sales.Customer table.</span>"
            ],
            "metadata": {
                "azdata_cell_guid": "6d9c45c7-2d0a-41cd-b7ac-a2e2e07e9d82"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT cus.CustomerID, cus.StoreID, cus.AccountNumber\r\n",
                "FROM Sales.Customer AS cus;"
            ],
            "metadata": {
                "azdata_cell_guid": "8db8397b-33f7-40db-ab3b-e2d8f1b0c921",
                "language": "sql",
                "tags": []
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                "2\\. Write a SELECT statement that lists the name, product number, and color of each product from the Production.Product table."
            ],
            "metadata": {
                "azdata_cell_guid": "b46148b8-95d3-464c-92a0-d9ee3a97d611"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT prod.Name, prod.Color\r\n",
                "FROM Production.Product as prod;"
            ],
            "metadata": {
                "azdata_cell_guid": "2f6ac9db-ae85-485a-b15d-5a11dbaa80ab",
                "language": "sql"
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                "3\\. Write a SELECT statement that lists the customer ID numbers and sales order ID numbers from the Sales.SalesOrderHeader table."
            ],
            "metadata": {
                "azdata_cell_guid": "191b8390-b3f2-4531-b60f-8e54230f11bf"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT sales.CustomerID,sales.SalesOrderID\r\n",
                "FROM Sales.SalesOrderHeader AS sales;"
            ],
            "metadata": {
                "azdata_cell_guid": "06d2d286-7bb9-4155-9bcf-d0b15315a602",
                "language": "sql"
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                "4\\. Switch to the WideWorldImporters database for the remaining questions in this exercise. Write a SELECT statement that lists only the StateProvinceCode and the StateProvinceName from the Application.StateProvinces table. Include a literal value as the first column in the SELECT list: 'State Abbr/Name:'."
            ],
            "metadata": {
                "azdata_cell_guid": "fddaa848-34ba-46e4-b82d-42f76f41186e"
            },
            "attachments": {}
        },
        {
            "cell_type": "code",
            "source": [
                "SELECT 'omaewa mo shindeiru' AS \"nani\", StateProvinceCode, StateProvinceName\r\n",
                "from Application.StateProvinces;"
            ],
            "metadata": {
                "azdata_cell_guid": "b58098e2-a3e0-4e65-9c44-5f8bcee03373",
                "language": "sql",
                "tags": []
            },
            "outputs": [],
            "execution_count": null
        },
        {
            "cell_type": "markdown",
            "source": [
                ""
            ],
            "metadata": {
                "azdata_cell_guid": "ba26f005-738a-4c40-9baf-50d6dc268993"
            },
            "attachments": {}
        }
    ]
}
