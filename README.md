# 🗄️ Customer Churn Analysis: SQL Data Preparation & Querying 📉

This repository contains SQL scripts and documentation for a database project focused on **Customer Churn Analysis**. This project forms the foundational data layer for understanding customer attrition, enabling subsequent analysis and dashboard creation (like the Power BI dashboards demonstrated in accompanying visuals).

## ✨ Project Overview

The goal of this SQL project is to:

* **Structure and Manage Customer Data:** Define tables to store comprehensive customer information.
* **Identify Churn Indicators:** Store and manage data points relevant to predicting and understanding customer churn.
* **Enable Data Extraction:** Provide clear SQL queries for extracting, transforming, and loading data for business intelligence tools and further analysis.
* **Support Churn Insights:** Facilitate the exploration of relationships between customer attributes, service usage, and churn behavior directly within the database.

-- 1. Select all columns from a table
SELECT * 
FROM table_name;

-- 2. Select specific columns, with alias
SELECT id, name AS full_name
FROM users;

-- 3. Filter rows
SELECT name, salary
FROM employees
WHERE department = 'IT'
  AND salary > 50000;

-- 4. Distinct values
SELECT DISTINCT department
FROM employees;

-- 5. Sort results
SELECT name, created_at
FROM posts
ORDER BY created_at DESC;

-- 6. Limit & Offset (pagination)
SELECT *
FROM orders
ORDER BY order_date DESC
LIMIT 10
OFFSET 20;

-- 7. Aggregation and grouping
SELECT department, COUNT(*) AS num_emp, AVG(salary) AS avg_sal
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;

-- 8. Join tables
SELECT o.id AS order_id, u.name AS customer
FROM orders o
INNER JOIN users u ON o.user_id = u.id;

### `Services` Table (Conceptual Example)
Details about services subscribed by customers.

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

     Summary
Clauses: SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY, LIMIT / OFFSET

Commands: INSERT, UPDATE, DELETE, CREATE TABLE, ALTER TABLE, DROP TABLE

Functions & Expressions: COUNT(), SUM(), AVG(), MIN(), MAX(), ROUND(), CASE, arithmetic ops (+, -, *, /), string ops


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
