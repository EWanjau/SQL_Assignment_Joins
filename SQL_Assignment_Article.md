# Connecting Power BI to SQL Databases

Power BI is a business intelligence tool made for extracting, organizing, and visualizing data in business. The goal is to take raw data and get insights after processing and analysis. Data can be in various forms — spreadsheets, databases, cloud-hosted files, and more.

In the past, organizations stored data in files and folders, but now other forms of data storage are favored. Technological improvements have made applications mainstream in business, and data storage has changed significantly alongside them. The modern business landscape demands real-time data access, concurrent collaboration, and structured storage solutions. The need for database storage cannot be ignored — databases offer ease of access, security, and concurrency.

![Power BI Overview Diagram](image-placeholder.png)



## Types of Databases

Databases are categorized into two types depending on the structure they use to store data:

- **Structured Query Language (SQL):** Use relational tables to store information. Examples: MySQL, PostgreSQL.
- **No-SQL (Non-relational):** Use other means such as JSON, objects, etc. Examples: Redis, MongoDB.

SQL-based databases are ideal for working with structured data that can be combined through relationships. They allow for data cleaning and processing to produce accurate data that is later used for analysis.

![SQL vs NoSQL Comparison Diagram](image-placeholder.png)



## 1. Connecting Power BI to a Local PostgreSQL Database

PostgreSQL is a structured query database used to develop modern applications and online systems. Power BI is capable of importing and loading data from various sources including Excel files, CSV files, database files, and cloud storage.

### Database Connections

Database systems can be hosted on:

- **Local servers** — the computer a user is operating (localhost)
- **Online database services** — such as AWS, GCP, Aiven, DB Clusters, etc.

### Steps to Connect Power BI to a Locally Hosted Database

![Power BI Get Data Screen](image-placeholder.png)

1. Open Power BI and select **Get Data** on the top bar menu.

2. Scroll through the list of sources and click **More Options**. Select **Databases**, then choose **PostgreSQL Database** on the right and click **Connect**.

3. Enter the server as `localhost` and provide the name of the database you are connecting to.

4. Provide the database username and password.

5. Once the connection is successful, Power BI loads all the tables you have created in the database. Select the tables you wish to work on and load the data.

6. Open the **Model View** and inspect the tables.

7. Open **Power Query** to check for data consistency and correct any errors in the data.

8. Once cleaning is done, create a relationship between the tables using the common column (`id`) between them.

> Relationships allow you to analyse data that is in different tables but related to the main object.


## 2. Connecting Power BI to a Cloud PostgreSQL Database (Aiven)

It is standard practice for online servers that host databases to establish security protocols. To connect Power BI to a cloud-hosted database, you must establish a secure connection using an encryption certificate. Only a computer with this certificate can connect to the server.

### Part 1: Connect to the Database Server

For Aiven cloud service, follow these steps:

![Aiven Service Overview Screenshot](image-placeholder.png)

1. Select the database service in Aiven you wish to connect to and activate it. In this case, the **PostgreSQL Database** service.

2. Click the **Service Overview** to display the service details.

3. Click the **Download** button on the CA Certificate and save it to your PC.

4. Rename the downloaded file from `ca.pem` → `ca.crt`.

5. Double-click the `ca.crt` file and click **Install Certificate** on your PC.

6. Select **Local Machine** as the installation location.

7. Select the certificate store: choose **Trusted Root Certification Authorities**.

8. Click **Finish** — setup is complete.

### Part 2: Login to the Database

1. Gather the following details from the Aiven Overview Page:
   - Port
   - Host Name
   - Database Name
   - Username
   - Password

2. Open Power BI and click **Get Data**.

3. In the list, select **More** and choose **PostgreSQL Database**.

4. Enter the **Server Name** and **Database Name** using the values copied from Aiven. Leave the data connectivity mode on the default **Import** option.

   > **Note:** The server name uses the format `hostname:port_number`.

5. Insert the username and password, then click **Connect**.

![Power BI PostgreSQL Connection Dialog](image-placeholder.png)


## 3. Loading Tables and Creating Relationships in Power BI

A successful connection displays the tables stored on the database. In this case: **Customers**, **Products**, **Sales**, and **Inventory**.

1. Select the tables you require and load them into Power BI.

2. Open **Power Query** and inspect the data. Clean inconsistent data, address any duplicates and null values, then save changes.

3. Open the **Model View** and create relationships between tables using common columns — typically primary and foreign keys. In some cases, Power BI selects relationships automatically. Review and delete any unwanted connections.

![Power BI Model View with Table Relationships](image-placeholder.png)

### What is Data Modeling?

Data modeling is the process of defining how data is stored, structured, and related within a database or analytics tool like Power BI. Think of it as creating a **blueprint** for your data so that different pieces of information can talk to each other.

### Why Relationships Matter

In a well-designed system, data is split into multiple tables — **Customers**, **Inventory**, **Sales**, and **Products** — to avoid repetition and keep things organized. Relationships are the bridges that connect these tables using common fields, such as a Product ID.

Without these connections, data exists in isolated containers. Relationships allow you to:

- **Combine Data** — see the name of a product next to its sales figures.
- **Analyze Correctly** — when you filter by category, sales numbers update to show only that category.
- **Support Accurate Reporting** — prevent double-counting or mismatched information that leads to incorrect business decisions.

In Power BI, the data model is what makes your dashboards interactive. When you click a slice of a pie chart, the rest of the report updates because of the underlying relationships.

### Types of Relationships

Once you've identified the connecting field, you must define the direction and cardinality of the relationship. The three most common types are:

| Type | Description | Example |
|------|-------------|---------|
| **One-to-Many** | The gold standard — one record relates to many | One product can be sold many times |
| **One-to-One** | Used for splitting large tables | Employees and Employee Sensitive Details |
| **Many-to-Many** | Complex — multiple items on both sides relate | Multiple products in multiple orders |


## 4. Conclusion: The Role of SQL in Power BI

SQL (Structured Query Language) is often considered the "assist" for high-level Power BI work. While Power BI has great built-in tools for connecting to data, SQL allows you to handle the heavy lifting before the data even reaches your report.

> If Power BI is the kitchen where you plate the meal, SQL is the prep station where you chop, wash, and organize the ingredients.

### How SQL Empowers the Analyst

- **Precise Retrieval:** Instead of importing a massive table with 100 columns you don't need, you can write a `SELECT` statement to bring in only the specific columns required.

- **Efficient Filtering:** Using a `WHERE` clause in SQL filters the data at the source (the database). This is much faster than importing millions of rows and filtering them inside Power BI.

- **Pre-Aggregated Data:** You can use `GROUP BY` to sum up sales or average scores in the database. This creates a smaller dataset that makes your Power BI dashboards more responsive.

- **Data Transformation:** SQL is powerful for cleaning messy data — renaming columns, handling null values, or combining strings — before the data model is even built.

![SQL Query Workflow Diagram](image-placeholder.png)
