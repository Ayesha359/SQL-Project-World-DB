# 🗄️ Customer Churn Analysis: SQL Data Preparation & Querying 📉

This repository contains SQL scripts and documentation for a database project focused on **Customer Churn Analysis**. This project forms the foundational data layer for understanding customer attrition, enabling subsequent analysis and dashboard creation (like the Power BI dashboards demonstrated in accompanying visuals).

## ✨ Project Overview

The goal of this SQL project is to:

* **Structure and Manage Customer Data:** Define tables to store comprehensive customer information.
* **Identify Churn Indicators:** Store and manage data points relevant to predicting and understanding customer churn.
* **Enable Data Extraction:** Provide clear SQL queries for extracting, transforming, and loading data for business intelligence tools and further analysis.
* **Support Churn Insights:** Facilitate the exploration of relationships between customer attributes, service usage, and churn behavior directly within the database.

## 🛠️ Key Components & Data Schema (Conceptual)

While specific table names and structures may vary, a typical database for customer churn analysis would involve tables like:

### `Customers` Table (Conceptual Example)
Stores core customer demographic and account information.
| Column Name      | Data Type | Description                               | Example Values           |
| :--------------- | :-------- | :---------------------------------------- | :----------------------- |
| `CustomerID`     | INT       | Unique identifier for each customer       | 1001, 1002               |
| `Gender`         | VARCHAR   | Male/Female                               | 'Male', 'Female'         |
| `Age`            | INT       | Customer's age                            | 25, 45                   |
| `MaritalStatus`  | VARCHAR   | Marital status (e.g., 'Single', 'Married') | 'Single', 'Partner'      |
| `Dependents`     | BIT       | Does customer have dependents? (True/False) | 1 (True), 0 (False)      |
| `TenureMonths`   | INT       | Number of months customer has stayed      | 12, 60                   |
| `TotalCharges`   | DECIMAL   | Total amount charged to the customer      | 123.45, 9876.54          |
| `Churn`          | BIT       | Did the customer churn? (1=Yes, 0=No)     | 1, 0                     |

### `Services` Table (Conceptual Example)
Details about services subscribed by customers.
| Column Name        | Data Type | Description                                   |
| :----------------- | :-------- | :-------------------------------------------- |
| `CustomerID`       | INT       | Foreign key linking to `Customers`            |
| `PhoneService`     | BIT       | Has phone service?                            |
| `MultipleLines`    | BIT       | Has multiple lines?                           |
| `InternetService`  | VARCHAR   | Type of internet service (e.g., 'DSL', 'Fiber optic', 'No') |
| `OnlineSecurity`   | BIT       | Has online security?                          |
| `OnlineBackup`     | BIT       | Has online backup?                            |
| `DeviceProtection` | BIT       | Has device protection?                        |
| `TechSupport`      | BIT       | Has tech support?                             |
| `StreamingTV`      | BIT       | Has streaming TV?                             |
| `StreamingMovies`  | BIT       | Has streaming movies?                         |

### `Contracts` Table (Conceptual Example)
Details about customer contracts and billing.
| Column Name      | Data Type | Description                                   |
| :--------------- | :-------- | :-------------------------------------------- |
| `CustomerID`     | INT       | Foreign key linking to `Customers`            |
| `ContractType`   | VARCHAR   | Type of contract (e.g., 'Month-to-month', 'One year', 'Two year') |
| `PaperlessBilling` | BIT       | Is paperless billing enabled?                 |
| `PaymentMethod`  | VARCHAR   | How the customer pays (e.g., 'Electronic check', 'Mailed check') |
| `MonthlyCharges` | DECIMAL   | Monthly recurring charges                     |

## 💻 Example SQL Commands & Queries

This section demonstrates common SQL operations relevant to churn analysis:

* **Retrieve all churned customers with their contract type:**
    ```sql
    SELECT c.CustomerID, c.Gender, co.ContractType
    FROM Customers c
    INNER JOIN Contracts co ON c.CustomerID = co.CustomerID
    WHERE c.Churn = 1;
    ```

* **Calculate churn rate by contract type:**
    ```sql
    SELECT
        ContractType,
        COUNT(CASE WHEN c.Churn = 1 THEN c.CustomerID END) AS ChurnedCustomers,
        COUNT(c.CustomerID) AS TotalCustomers,
        CAST(COUNT(CASE WHEN c.Churn = 1 THEN c.CustomerID END) AS DECIMAL) * 100 / COUNT(c.CustomerID) AS ChurnRate_Percentage
    FROM Customers c
    INNER JOIN Contracts co ON c.CustomerID = co.CustomerID
    GROUP BY ContractType
    ORDER BY ChurnRate_Percentage DESC;
    ```

* **Find customers with Fiber Optic Internet who have churned:**
    ```sql
    SELECT c.CustomerID, c.Age, c.TenureMonths
    FROM Customers c
    INNER JOIN Services s ON c.CustomerID = s.CustomerID
    WHERE c.Churn = 1 AND s.InternetService = 'Fiber optic';
    ```

* **Update a customer's churn status (e.g., if re-engaged):**
    ```sql
    UPDATE Customers
    SET Churn = 0 -- Set to 0 for retained
    WHERE CustomerID = 12345;
    ```

## 🚀 Getting Started (Conceptual)

To set up a similar database:

1.  **Database System:** Choose a relational database system (e.g., MySQL, PostgreSQL, SQL Server, SQLite).
2.  **Schema Creation:** Run DDL (Data Definition Language) scripts to create the `Customers`, `Services`, and `Contracts` tables (or similar tables relevant to your data).
3.  **Data Loading:** Import your raw customer churn data into these tables using `INSERT` statements or bulk import tools.
4.  **Query & Analyze:** Execute SQL queries to analyze the data, extract insights, and prepare data for BI tools.


![Screenshot 2025-06-12 152803](https://github.com/user-attachments/assets/71698684-dbaf-4241-b931-186216d94a6d)

![Screenshot 2025-06-12 153542](https://github.com/user-attachments/assets/a42972e7-45b3-47c6-8454-63a69cb84c65)

![Screenshot 2025-06-12 153737](https://github.com/user-attachments/assets/d34d4302-18c0-412f-a2b0-ff44e0f510c2)

![Screenshot 2025-06-12 154401](https://github.com/user-attachments/assets/5b6894ea-dda5-4691-9374-c5b4da606b75)







---
