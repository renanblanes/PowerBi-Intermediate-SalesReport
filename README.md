# PowerBi-Intermediate-SalesReport
## Project Overview
### Report Methodology
This report utilizes the S.M.A.R.T methodology, which aims to make the report goal Specific, Measurable, Achievable, Relevant and Time-bound

### Goals
The primary objective is to answer two business questions:
1. Where are we losing money? Identify products categories or geografic location where the **YoY declined more than 10%**
2. Why are we losing money? Analyse the possible **root factor(s)* for the decline

### Deliverables
1. A Interactive Dashboard that tracks: Gross Revenue, Margin, Customer Lifetime Value, Revenue YoY/MoM
2. Recomendations for the Sales Department



# Data Source & Cleaning
Data gathered from **[Kaggle](https://www.kaggle.com/datasets/yashyennewar/product-sales-dataset-2023-2024)**

The **[RAW FILE](https://drive.google.com/uc?export=download&id=1WQ-ooANAGiREKENRF8otLXVyWk2QESo_)** was uploaded on GoogleDrive for easy access to anyone who wants to recreate this project
**AND to connect Power BI directly to a remote data source**

### **Initial Data Quality Fixes (Power Query M)**

* **Date Locale:** The `Order_Date` column, initially in M/D/Y text format, was converted to the proper Date type using the **English (United States) Locale** to prevent regional misinterpretation.
* **Decimal Locale:** The `Unit_Price, Revenue, Profit` columns were corrected to properly interpret the dot (`.`) as the decimal separator, resolving numerical conversion errors.

## Data Modeling & Schema Design

Following best practices, the raw transactional data was structured into a **Star Schema** with the following dimensions



### **Fact Table: Sales**

* Contains all transactional data (`Revenue`, `Profit`, `Quantity`).
* All dimensional keys (`Customer_ID`, `Product_ID`, `Geography_ID`, `Date_Key`) were added as integer keys and used for creating one-to-many relationships.

### **Dimension Tables (Feature Engineering & Columns Selected)**

**Dim_Customer**
`Customer_ID`, `First_Name`, `Last_Name`, `Email`
**Steps** 
1. Created `Customer_ID` via **Index Column**
2. Split `Full_Name` into `First_Name` and `Last_Name` using the **Leftmost Delimiter** split.
3. Generated a proxy `Email` column for demonstration purposes since the original dataset lacked one, it does not represent a real step that woulb be taken on a real job

**Dim_Product**
`Product_ID`, `Category`, `Sub-Category`, `Product Name`, `Unit Price`
1. Created `Product_ID` via an **Index Column**.
2. Ensured hierarchy purity: `Category` and `Sub-Category`.

**Dim_Geography**
`City ID`, `City`, `State`, `Region`, `Country` 
1. Created `City ID` via an **Index Column** to serve as the key for linking location details.

**Dim_Date** 
Created using this [**M-language script**](https://drive.google.com/uc?export=download&id=1rR4Nc1pxLMuv47-ysNthejsHae_X1yRQ) to ensure a complete, contiguous date range for accurate **YoY/MoM** calculations.


