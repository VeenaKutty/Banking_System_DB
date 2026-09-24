# Banking System Database

## Project Overview

The **Banking System Database** is a relational database project developed using **MySQL** to manage and analyze core banking operations.

The project models a banking environment where customers can maintain multiple accounts, perform financial transactions, interact with branches, and hold loans.

The database is designed to support both **operational data management** and **business analysis**, allowing banking-related information to be transformed into meaningful insights using SQL.

---

## Business Objective

Banks generate large volumes of structured data across customers, accounts, transactions, branches, and loans.

The objective of this project is to build a centralized relational database that can:

* Maintain customer information
* Manage customer bank accounts
* Track financial transactions
* Manage branch-level information
* Track customer loans
* Analyze customer financial activity
* Identify high-value customers and accounts
* Analyze branch performance
* Analyze transaction activity
* Analyze loan portfolios
* Generate reusable business-level datasets using SQL Views

---

## Business Problem

A banking organization needs a structured system to manage and analyze information across multiple business entities.

Without a properly designed relational database, it becomes difficult to answer questions such as:

* Which customers have the highest account balances?
* Which branches manage the largest number of accounts?
* What is the total transaction volume?
* Which transaction types generate the highest value?
* Which customers have multiple accounts?
* Which customers have significant loan exposure?
* Which branches have the highest financial activity?
* Which accounts have balances above the overall average?
* How does transaction activity vary over time?

This project addresses these requirements through a relational database and SQL-based business analysis.

---

# Project Architecture

```text
                    BANKING SYSTEM
                          |
        -------------------------------------
        |          |          |             |
        v          v          v             v
    Customers   Accounts   Transactions   Loans
        |          |          |             |
        |          |          |             |
        |          v          |             |
        |       Branches       |             |
        |                     |             |
        ----------- SQL Analysis ------------
                          |
                          v
                 Business Insights
```

---

# Database Design

The database is named:

```text
BANKING_SYSTEMDB
```

The system contains the following major entities:

| Entity       | Purpose                          |
| ------------ | -------------------------------- |
| CUSTOMERS    | Stores customer information      |
| ACCOUNTS     | Stores customer bank accounts    |
| TRANSACTIONS | Stores financial transactions    |
| BRANCHES     | Stores branch information        |
| LOANS        | Stores customer loan information |

---

# Entity Relationships

The major relationships in the database are:

```text
CUSTOMERS
    |
    | 1 : N
    v
ACCOUNTS
    |
    | 1 : N
    v
TRANSACTIONS


BRANCHES
    |
    | 1 : N
    v
ACCOUNTS


CUSTOMERS
    |
    | 1 : N
    v
LOANS
```

### Relationship Summary

* One customer can have multiple accounts.
* One account can have multiple transactions.
* One branch can manage multiple accounts.
* One customer can have multiple loans.
* Accounts are associated with branches through branch information.

---

# Data Model

## Customers

The `CUSTOMERS` table stores customer-level information.

Key information includes:

* Customer ID
* First Name
* Last Name
* Email
* Phone
* Birth Date

The customer entity acts as a central entity for account and loan relationships.

---

## Accounts

The `ACCOUNTS` table stores banking account information.

Key information includes:

* Account ID
* Account Type
* Balance
* Customer ID
* Branch ID
* Account Creation Date

This table connects customers with their banking accounts and branches.

---

## Transactions

The `TRANSACTIONS` table records financial activities performed through customer accounts.

Key information includes:

* Transaction ID
* Transaction Date
* Transaction Amount
* Transaction Type
* Account ID

This table enables analysis of transaction volume, transaction value, and account activity.

---

## Branches

The `BRANCHES` table stores information about banking branches.

Key information includes:

* Branch ID
* Branch Name
* Branch Address
* Branch Phone

The branch information allows the organization to perform branch-level analysis.

---

## Loans

The `LOANS` table stores information related to customer loans.

Key information includes:

* Loan ID
* Loan Amount
* Interest Rate
* Start Date
* End Date
* Customer ID

This data can be used to analyze the bank's loan portfolio and customer loan exposure.

---

# Technology Stack

| Technology      | Usage                                  |
| --------------- | -------------------------------------- |
| MySQL           | Database development                   |
| SQL             | Data management and analysis           |
| MySQL Workbench | Database modeling and execution        |
| GitHub          | Version control and project management |

---

# Project Workflow

```text
Business Requirement
        |
        v
Database Design
        |
        v
ER Model
        |
        v
Database Creation
        |
        v
Table Creation
        |
        v
Data Population
        |
        v
Data Validation
        |
        v
SQL Analysis
        |
        +----------------+
        |                |
        v                v
   Operational       Business
     Queries          Analysis
        |                |
        +-------+--------+
                |
                v
        Banking Insights
```

---

# Data Analysis

The database supports analysis across multiple banking dimensions.

## Customer Analysis

Customer-level analysis can be used to identify:

* Total number of customers
* Customer demographic information
* Customers with multiple accounts
* Customers with incomplete information
* Customers with high account balances
* Customers with significant loan exposure

---

## Account Analysis

Account analysis provides insights into:

* Number of accounts
* Account types
* Total account balance
* Average account balance
* Minimum and maximum balances
* Customer account ownership
* Branch-level account distribution

Example business question:

> Which customers have account balances above the overall average balance?

```sql
SELECT *
FROM ACCOUNTS
WHERE BALANCE > (
    SELECT AVG(BALANCE)
    FROM ACCOUNTS
);
```

---

# Transaction Analysis

Transaction data can be analyzed to understand banking activity.

Key metrics include:

* Total transaction value
* Number of transactions
* Average transaction amount
* Maximum transaction amount
* Minimum transaction amount
* Transaction type distribution
* Account-level transaction activity
* Time-based transaction activity

Example business questions:

```text
Which account has the highest transaction activity?

Which transaction type has the highest transaction value?

What is the average transaction amount?

What is the monthly transaction volume?
```

---

# Branch Performance Analysis

Branch-level analysis helps evaluate banking activity across locations.

Possible KPIs include:

| KPI                | Business Purpose                |
| ------------------ | ------------------------------- |
| Total Accounts     | Measures account distribution   |
| Total Balance      | Measures deposits held          |
| Average Balance    | Measures customer account value |
| Customer Count     | Measures customer base          |
| Transaction Volume | Measures banking activity       |
| Loan Exposure      | Measures lending activity       |

This allows branch-level comparison using SQL aggregation and relational analysis.

---

# Loan Portfolio Analysis

The loan data can be used to analyze:

* Total loan amount
* Average loan amount
* Maximum loan amount
* Interest rates
* Customer loan exposure
* Number of loans per customer
* Loan duration
* Active and completed loans

Example business questions:

```text
Which customer has the highest loan exposure?

What is the average loan amount?

Which customers have multiple loans?

Which loan has the highest interest rate?

What is the total value of the loan portfolio?
```

---

# Advanced SQL Analysis

The project uses SQL beyond basic CRUD operations to generate business insights.

### Joins

Multiple tables can be combined to create comprehensive datasets.

Example:

```text
Customers
    +
Accounts
    +
Branches
    +
Transactions
```

This allows customer-level financial activity to be analyzed together with account and branch information.

---

### Subqueries

Subqueries are used for dynamic business comparisons.

For example:

```sql
SELECT *
FROM ACCOUNTS
WHERE BALANCE > (
    SELECT AVG(BALANCE)
    FROM ACCOUNTS
);
```

This identifies accounts whose balance is higher than the overall average.

---

### Views

Reusable analytical views are created to simplify frequently required business queries.

Examples include:

```text
CUSTOMER_DETAILS
CUSTOMER_ACCOUNTS
CUSTOMER_ACCOUNT_SUMMARY
TRANSACTION_SUMMARY
BRANCH_PERFORMANCE
LOAN_SUMMARY
```

These views transform complex SQL queries into reusable datasets for reporting and analysis.

---

### Window Functions

Window functions are used for advanced analytical requirements such as:

* Ranking customers
* Ranking accounts
* Ranking loans
* Running transaction totals
* Comparing current and previous transactions
* Comparing current and next records

Functions used include:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER()
```

---

# SQL Functions

The project also applies SQL functions for data transformation and analysis.

### String Functions

Used for customer and text-data transformation.

Examples:

```text
CONCAT()
UPPER()
LOWER()
```

### Mathematical Functions

Used for financial calculations and aggregation.

Examples:

```text
SUM()
AVG()
MIN()
MAX()
ROUND()
COUNT()
```

### Date and Time Functions

Used for transaction, account, customer, and loan analysis.

Examples include:

```text
YEAR()
DATE_FORMAT()
DATE_ADD()
DATE_SUB()
```

---

# Key Business KPIs

The database can support several banking KPIs.

### Customer KPIs

```text
Total Customers
Customers with Multiple Accounts
Customers with Loans
High-Value Customers
```

### Account KPIs

```text
Total Accounts
Total Account Balance
Average Account Balance
Maximum Account Balance
Accounts by Type
```

### Transaction KPIs

```text
Total Transactions
Total Transaction Value
Average Transaction Value
Transaction Volume
Transaction Value by Type
```

### Branch KPIs

```text
Total Accounts by Branch
Total Balance by Branch
Average Balance by Branch
Transaction Activity by Branch
```

### Loan KPIs

```text
Total Loans
Total Loan Value
Average Loan Amount
Average Interest Rate
Customer Loan Exposure
```

---

# Example Business Insights

Using the database, management could generate insights such as:

```text
1. Identify customers with unusually high account balances.

2. Identify branches managing the highest number of accounts.

3. Determine the branches with the highest total deposits.

4. Identify accounts with unusually high transaction activity.

5. Analyze the distribution of transaction types.

6. Identify customers with multiple banking products.

7. Determine customers with significant loan exposure.

8. Analyze average loan amounts and interest rates.

9. Rank customers based on their total account balances.

10. Analyze transaction activity over time.
```

These analyses provide a foundation for banking performance reporting and can be further connected to visualization tools such as Power BI or Tableau.

---

# Repository Structure

```text
Banking_System_DB/
│
├── Banking_SystemDB.sql
│
├── ER_DIAGRAM.mwb
│
└── README.md
```

### Banking_SystemDB.sql

Contains the SQL implementation of the banking database, including:

* Database creation
* Table creation
* Constraints
* Data insertion
* Data manipulation
* Data retrieval
* Business analysis
* SQL functions
* Joins
* Subqueries
* Views
* Window functions

### ER_DIAGRAM.mwb

Contains the MySQL Workbench data model representing the relationships between the banking entities.

---

# How to Run the Project

## Prerequisites

Install:

* MySQL Server
* MySQL Workbench

## Clone Repository

```bash
git clone https://github.com/VeenaKutty/Banking_System_DB.git
```

## Open the Project

Open:

```text
Banking_SystemDB.sql
```

using MySQL Workbench.

## Execute the SQL Script

Run the script to create the database, tables, relationships, sample data, and analytical queries.

Then execute:

```sql
USE BANKING_SYSTEMDB;

SHOW TABLES;
```

---

# Potential Extensions

The current database can be extended into a complete banking analytics solution.

Possible extensions include:

### Data Analytics

* Python-based exploratory data analysis
* Customer segmentation
* Transaction trend analysis
* Financial risk analysis

### Business Intelligence

* Power BI banking dashboard
* Customer 360 dashboard
* Branch performance dashboard
* Transaction analytics dashboard
* Loan portfolio dashboard

### Machine Learning

Potential ML applications include:

* Customer churn prediction
* Loan default prediction
* Fraud detection
* Customer segmentation
* Credit risk prediction

### Backend Integration

The database can also be integrated with:

```text
Python
FastAPI
Flask
Streamlit
Power BI
```

to build a complete data-driven banking application.

---

# Project Outcome

This project demonstrates how a relational database can be designed around a real-world banking scenario and transformed into a foundation for business intelligence and advanced analytics.

The database provides a structured environment for managing:

```text
Customers
    ↓
Accounts
    ↓
Transactions

Customers
    ↓
Loans

Branches
    ↓
Accounts
```

The resulting SQL layer enables operational queries, analytical reporting, KPI generation, and advanced business analysis.

---

# Future Roadmap

```text
MySQL Database
       |
       v
SQL Business Analysis
       |
       v
Python ETL / Analysis
       |
       v
Power BI Dashboard
       |
       v
Machine Learning
       |
       v
End-to-End Banking Analytics Platform
```

---

# Author

**Veena Kutty**

Data Science & Data Analytics Trainer

GitHub: [VeenaKutty](https://github.com/VeenaKutty)

---

# Repository

**Banking System Database**

[View Project on GitHub](https://github.com/VeenaKutty/Banking_System_DB)
