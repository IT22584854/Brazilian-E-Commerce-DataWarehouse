# 📦 Brazilian E-Commerce DataWarehouse Project
## 📘 Project Summary
This repository contains a comprehensive data warehousing and business intelligence (BI) solution. The project involves designing a star schema-based data warehouse using Microsoft SQL Server, developing an ETL pipeline with SQL Server Integration Services (SSIS), building an OLAP cube using SQL Server Analysis Services (SSAS), and visualizing insights through Power BI.
## 🎯 Project Objectives
- Integrate structured data from:
- the Brazilian E-Commerce transactional SQL database
- external CSV file
- Design a star schema data warehouse optimized for analytical workloads
- Develop a complete ETL process using SSIS
- Handle data quality, data integration, and transformation
- Build a multidimensional OLAP Cube using SSAS for efficient querying
- Generate interactive dashboards and visual reports using Power BI and Excel.

# Solution Architecture
![image](https://github.com/user-attachments/assets/1e5bdf17-08d6-4f43-a82b-f1ab29b4f66a)

## 📂 Data Sources
- CSV file: Olist_Location.csv
- Sql Server: Olist_customer Table, Olist_orders Table, Olist_product_dataset

These sources were ingested into a staging database before being transformed and loaded into the final dimensional model.

## 🛢️ Database Design
### 📍 Staging Area
The staging database mirrors the raw data to perform cleansing, integration, and transformation independently of the source systems.

#### Tables in Staging:
StgCustomers

StgLocation

StgOrder

StgProduct

-----
## 🧱 Data Warehouse Schema (Star Schema)
 ![image](https://github.com/user-attachments/assets/125ca381-a55d-4b42-b6e0-0ed5abf955af)

### ⭐ Fact Table
•	FactOrder: Combines orders and line item data with foreign keys to all dimensions.

### 🧩 Dimension Tables
DimCustomer: 	Created using multiple staging tables: stgCustomers, StgLocation 
DimProduct:	Created using StgProduct table
DimDate:	Generated manually using SQL script (no source data contained date dimension)

-------
## 🔁 ETL Process Using SSIS

### 1. Extract
- Loaded data from SQL Server and CSV file into the staging area.

### 2. Transform
- Product dimension combines multiple product-related staging tables.
- Data Cleansing: Added transformations to remove null values from the StgProduct Table
- Dimension Types:
  - Hierarchical Dimension: Date – all the hierarchies in date 
  - Slowly Changing Dimension: Customer – Customer_city, Customer_state, age

### 3. Load
- Data was loaded into dimension tables first, followed by the FactOrder table.
- Lookup transformations were used to retrieve surrogate keys from dimension tables.

---
# 📊 SSAS OLAP Cube Design

-	Customer Dimension
-	Product Dimension
-	Date Dimension

Each dimension includes a key column and descriptive attributes.

🧮 Fact Measure Group:

-	FactOrder: contains all measures used for multidimensional analysis.

🧰 Cube Processing Workflow:

1.	Create SSAS Multidimensional project in Visual Studio
2.	Define Data Source and Data Source View (DSV)
3.	Add Dimensions and establish relationships
4.	Create and deploy Cube
5.	Process Cube to load data

# 🔍 OLAP Operations Demonstrated (via Excel)

- Slice	Filter data on a single dimension
- Dice	Filter using two or more dimensions
- Pivot	Rotate data axes for analysis

# 📈 Power BI Dashboards
- Matrix Visual Report
- Multi-Slicer Visuals
- Drill-Down Report
- Drill-Through Report

