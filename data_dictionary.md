# 📖 Data Dictionary — ElectroHub Sales Data

> This document provides a detailed description of all columns across all tables in the dataset.

---

## 📋 Table Overview

| Table Name | Type | Rows | Columns | Description |
|---|---|---|---|---|
| **Fact Table** (Sheet3) | Fact | 3,510 | 10 | Transactional sales data — one row per order |
| **Dim Customers** | Dimension | 50 | 7 | Customer demographics and contact info |
| **Dim Product** | Dimension | 30 | 4 | Product catalog with pricing |
| **Dim Promotion** | Dimension | 5 | 5 | Promotional campaigns and discount types |
| **Date Table 1** | Date | Auto | 1 | Primary calendar table for Period 1 filtering |
| **Date Table 2** | Date | Auto | 1 | Secondary calendar table for Period 2 filtering |
| **Measures Table** | Measures | — | — | DAX calculated measures |

---

## 📊 Fact Table (Sales Transactions)

| # | Column Name | Data Type | Description | Example |
|---|---|---|---|---|
| 1 | `Date (dd/mm/yyyy)` | Date | Transaction date in DD-MM-YYYY format | 04-02-2020 |
| 2 | `CustomerID` | Integer | FK → Dim Customers.Customer ID | 10 |
| 3 | `PromotionID` | Text | FK → Dim Promotion.PromotionID (0 = no promotion) | PR001 |
| 4 | `Product ID` | Text | FK → Dim Product.ProductID | P004 |
| 5 | `Units Sold` | Integer | Number of units purchased in the transaction | 2 |
| 6 | `Price Per Unit` | Currency (₹) | Selling price per unit | ₹79,999 |
| 7 | `Total Sales` | Currency (₹) | Calculated: Units Sold × Price Per Unit | ₹1,59,998 |
| 8 | `Discount Percentage` | Decimal | Discount rate applied (0–100%) | 20 |
| 9 | `Discount Value` | Currency (₹) | Calculated: Total Sales × Discount % | ₹31,999 |
| 10 | `Net Sales` | Currency (₹) | Calculated: Total Sales − Discount Value | ₹1,27,999 |

---

## 👥 Dim Customers

| # | Column Name | Data Type | Description | Example |
|---|---|---|---|---|
| 1 | `Customer ID` | Integer | **Primary Key** — Unique customer identifier | 1 |
| 2 | `Customer Name` | Text | Full name of the customer | Aarav Singh |
| 3 | `City` | Text | City of residence | Nagpur |
| 4 | `State` | Text | State of residence | Maharashtra |
| 5 | `Pincode` | Integer | Postal/ZIP code | 440001 |
| 6 | `EmailID` | Text | Customer email address | 1Aarav@gmail.com |
| 7 | `Phone Number` | Integer | Contact phone number | 860135097 |

---

## 📦 Dim Product

| # | Column Name | Data Type | Description | Example |
|---|---|---|---|---|
| 1 | `ProductID` | Text | **Primary Key** — Product identifier (P001–P030) | P001 |
| 2 | `Product Name` | Text | Product display name | Apple iPhone 14 |
| 3 | `Product Line` | Text | Product category/line | Electronics |
| 4 | `Price (INR)` | Currency (₹) | Standard retail price | ₹79,999 |

---

## 🏷️ Dim Promotion

| # | Column Name | Data Type | Description | Example |
|---|---|---|---|---|
| 1 | `PromotionID` | Text | **Primary Key** — Promotion identifier | PR001 |
| 2 | `Promotion Name` | Text | Campaign name | Summer Sale |
| 3 | `Ad Type` | Text | Marketing channel used | Email |
| 4 | `Coupon Code` | Text | Promotional coupon code | SUMMER21 |
| 5 | `Price Reduction Type` | Text | Type of discount offered | 20% off |

---

## 📐 DAX Measures (Measures Table)

| Measure Name | Formula | Purpose |
|---|---|---|
| `Quantity sold` | `CALCULATE(SUM('Fact Table'[Units Sold]), ALL('Date Table 1'), USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))` | Calculate units sold for Period 2 using inactive relationship |
| `Sum of Net Sales` | `CALCULATE(SUM('Fact Table'[Net sales]), ALL('Date Table 1'), USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))` | Calculate net sales for Period 2 using inactive relationship |
| `Total Profit` | `CALCULATE(SUM('Fact Table'[Profit]), All('Date Table 1'), USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))` | Calculate total profit for Period 2 using inactive relationship |

---

## 🔗 Relationships

```
Dim Product (ProductID)       ──── 1:* ────  Fact Table (Product ID)
Dim Customers (Customer ID)   ──── 1:* ────  Fact Table (CustomerID)
Dim Promotion (PromotionID)   ──── 1:* ────  Fact Table (PromotionID)
Date Table 1 (Date)           ──── 1:* ────  Fact Table (Date)         [ACTIVE]
Date Table 2 (Date)           ──── 1:* ────  Fact Table (Date)         [INACTIVE]
```

---

> **Note**: Date Table 1 controls Period 1 filtering. Date Table 2 is activated via `USERELATIONSHIP()` in DAX measures to enable independent Period 2 filtering.
