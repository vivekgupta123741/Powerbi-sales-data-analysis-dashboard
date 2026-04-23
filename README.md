<p align="center">
  <img src="https://img.shields.io/badge/Tool-Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/Tool-Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white" />
  <img src="https://img.shields.io/badge/Language-DAX-E97627?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Data%20Model-Star%20Schema-blueviolet?style=for-the-badge" />
</p>

<h1 align="center">📊 ElectroHub — Sales Data Analysis Dashboard</h1>

<p align="center">
  <b>An end-to-end Power BI project analyzing sales performance, profit trends, and customer behavior for a multi-city electronics retail business.</b>
</p>

<p align="center">
  <a href="#-project-overview">Overview</a> •
  <a href="#-problem-statement">Problem</a> •
  <a href="#-dataset-description">Dataset</a> •
  <a href="#-data-model">Data Model</a> •
  <a href="#-key-insights">Insights</a> •
  <a href="#-dashboard-features">Dashboard</a> •
  <a href="#-screenshots">Screenshots</a> •
  <a href="#-getting-started">Get Started</a>
</p>

---

## 📌 Project Overview

**ElectroHub** is a multi-city electronics retail business operating across major Indian cities including Nagpur, Bhopal, Ahmedabad, Indore, and more. This project analyzes **3,500+ sales transactions** spanning **2020–2024** to uncover actionable insights about sales performance, product profitability, customer behavior, and promotional effectiveness.

The interactive Power BI dashboard enables stakeholders to:
- Compare performance across **any two custom time periods**
- Identify **top/bottom performing products** by sales, profit, and quantity
- Analyze **city-wise sales distribution** across multiple states
- Understand the **relationship between sales and profit margins**
- Evaluate the **impact of promotional campaigns and discounts**

---

## 🎯 Problem Statement

ElectroHub's management needs a **data-driven approach** to answer critical business questions:

1. Which products are the **top/bottom 5** by Sales, Profit, and Quantity Sold?
2. How do **sales trends vary over time** (daily, monthly, quarterly, annually)?
3. What is the **relationship between sales and profit**?
4. How do **Sales/Profit/Quantity compare** between any two user-selected periods?
5. What is the **average discount** offered in each discount category?
6. What is the **total number of orders** processed?
7. Can we view **Sales/Profit/Discount/Net Sales** for each order with interactive filters?
8. How does **sales performance differ across cities**?

---

## 📁 Dataset Description

The dataset follows a **Star Schema** design pattern with **3 Dimension Tables** and **1 Fact Table**:

### Fact Table — `Fact_Sales` (3,510 rows × 10 columns)

| Column | Description | Type |
|--------|-------------|------|
| `Date (dd/mm/yyyy)` | Transaction date | Date |
| `CustomerID` | Foreign key → Dim Customers | Integer |
| `PromotionID` | Foreign key → Dim Promotion | Text |
| `Product ID` | Foreign key → Dim Product | Text |
| `Units Sold` | Quantity of items purchased | Integer |
| `Price Per Unit` | Selling price per unit (₹) | Currency |
| `Total Sales` | Units Sold × Price Per Unit (₹) | Currency |
| `Discount Percentage` | Applied discount rate | Decimal |
| `Discount Value` | Monetary discount amount (₹) | Currency |
| `Net Sales` | Total Sales − Discount Value (₹) | Currency |

### Dim Customers (50 rows × 7 columns)

| Column | Description |
|--------|-------------|
| `Customer ID` | Primary Key |
| `Customer Name` | Full name of the customer |
| `City` | City of residence (Nagpur, Bhopal, Indore, Ahmedabad, etc.) |
| `State` | State (Maharashtra, Madhya Pradesh, Gujarat, etc.) |
| `Pincode` | Postal code |
| `EmailID` | Customer email address |
| `Phone Number` | Contact number |

### Dim Product (30 rows × 4 columns)

| Column | Description |
|--------|-------------|
| `ProductID` | Primary Key (P001–P030) |
| `Product Name` | Product name (e.g., Apple iPhone 14, Samsung Galaxy S21) |
| `Product Line` | Category (Electronics) |
| `Price (INR)` | Standard retail price (₹) |

### Dim Promotion (5 rows × 5 columns)

| Column | Description |
|--------|-------------|
| `PromotionID` | Primary Key (PR001–PR005) |
| `Promotion Name` | Campaign name (Summer Sale, Festive Diwali, etc.) |
| `Ad Type` | Marketing channel (Email, Social Media, Website Banner) |
| `Coupon Code` | Promotional coupon code |
| `Price Reduction Type` | Discount type (20% off, Buy 1 Get 1 Free, etc.) |

---

## 🏗️ Data Model

The project uses a **Star Schema** with the Fact Table at the center, connected to three dimension tables and two date tables for period comparison:

<p align="center">
  <img src="screenshots/data_model.png" alt="Star Schema Data Model" width="800"/>
</p>

**Relationships:**
| From (Table) | To (Table) | Key | Cardinality |
|---|---|---|---|
| Fact Table → Dim Product | `Product ID` → `ProductID` | Many-to-One (*:1) | Active |
| Fact Table → Dim Customers | `CustomerID` → `Customer ID` | Many-to-One (*:1) | Active |
| Fact Table → Dim Promotion | `PromotionID` → `PromotionID` | Many-to-One (*:1) | Active |
| Fact Table → Date Table 1 | `Date` → `Date` | Many-to-One (*:1) | Active |
| Fact Table → Date Table 2 | `Date` → `Date` | Many-to-One (*:1) | Inactive (used via USERELATIONSHIP) |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard development, data modeling, interactive visualizations |
| **Microsoft Excel** | Data source, data cleaning, and preparation |
| **DAX (Data Analysis Expressions)** | Calculated measures, period comparison logic |
| **Power Query (M Language)** | Data transformation and loading (ETL) |
| **Star Schema Design** | Optimized data model for analytical queries |

---

## 🔑 Key Insights

### 💰 Revenue & Profitability
- **Total Revenue**: ₹122M generated across the full analysis period (2020–2024)
- **Total Profit**: ₹12.2M with an approximate **10% profit margin**
- **Total Units Sold**: 7,100+ units across 30 product SKUs
- **Total Orders**: 3,510 transactions processed

### 📈 Period Comparison Analysis
- **Period 1** (Jan 2020 – Mar 2023): ₹98M Sales | ₹9.8M Profit | 5.6K Units
- **Period 2** (May 2021 – Dec 2024): ₹81M Sales | ₹8.1M Profit | 4.8K Units
- The earlier period outperformed by **~21% in sales**, suggesting stronger initial market performance
- Extended comparison: ₹101M (up to May 2023) vs ₹122M (up to Jan 2024) — **20.8% cumulative growth**

### 📊 Sales Trends (2020–2024)
- **Peak monthly sales**: ₹0.65M recorded in **2023** — the highest single-period spike
- **2020**: Strong start at ₹0.55M, followed by consistent ₹0.49M–₹0.54M in 2021
- **2022**: Slight dip to ₹0.41M–₹0.49M range, indicating mid-cycle market correction
- **2023**: Recovery with sales rebounding to ₹0.43M–₹0.65M range
- **2024**: Stabilized around ₹0.48M with consistent performance
- Consistent ~10% profit-to-sales ratio maintained across all periods, indicating stable margins

### 🏙️ Geographic Distribution
- Sales span **10+ cities** across India including Delhi, Jaipur, Lucknow, Patna, Kolkata, Bhopal, Nagpur, Indore, Pune, Mumbai, Chennai, Visakhapatnam, and Bangalore
- Coverage across **multiple states**: Maharashtra, Madhya Pradesh, Gujarat, Rajasthan, UP, Bihar, West Bengal, Tamil Nadu, Andhra Pradesh, and Karnataka
- Key markets include **Nagpur, Bhopal, Ahmedabad, Indore, Mumbai, and Delhi**

### 🎯 Promotion & Discount Analysis
- **5 promotional campaigns** with varying discount impacts:
  - 🥇 **Weekend Flash Sale**: Highest avg. discount at ₹23K
  - 🥈 **Clearance Sale**: ₹15K average discount
  - 🥉 **Summer Sale**: ₹7K average discount
  - **New Year Special**: ₹3K average discount
  - **Festive Diwali**: ₹0K (no discount — full-price sales event)
- Promotions leverage multiple channels: Email, Social Media, and Website Banners

### 📈 Profit vs Net Sales Relationship
- **Strong positive linear correlation** between Profit and Net Sales
- As profit increases from ₹0K to ₹30K, net sales scale proportionally up to ₹300K
- Indicates **healthy and consistent profit margins** across all transaction sizes
- No significant outliers — demonstrates stable pricing and cost control

### 🏆 Top & Bottom Products Performance

**Top 5 Products by Sales:**
| Rank | Product | Sales |
|------|---------|-------|
| 🥇 | Apple iPhone 14 | ₹21.4M |
| 🥈 | Apple MacBook Air | ₹19.6M |
| 🥉 | Sony Bravia 55" TV | ₹19.4M |
| 4 | Samsung Galaxy S21 | ₹15.3M |
| 5 | HP Pavilion Laptop | ₹14.4M |

**Bottom 5 Products by Sales:**
| Rank | Product | Sales |
|------|---------|-------|
| 30 | Colgate Toothpaste | ₹0.03M |
| 29 | Dove Soap Pack | ₹0.08M |
| 28 | Nivea Body Lotion | ₹0.08M |
| 27 | L'Oreal Shampoo | ₹0.17M |
| 26 | Tupperware Lunch Box | ₹0.26M |

**Key Product Findings:**
- **Apple iPhone 14** dominates across all 3 metrics — #1 in Sales (₹21.4M), Quantity (281 units), and Profit (₹2.14M)
- Top 5 products by profit mirror the top 5 by sales — strong correlation between volume and profitability
- **Bottom performers** are low-cost FMCG items (Toothpaste, Soap, Shampoo) — selling at high volume (203-219 units) but generating minimal revenue
- Massive **800x revenue gap** between top product (₹21.4M) and bottom product (₹0.03M)

---

## 📊 Dashboard Features

### 🔄 Dynamic Period Comparison
- **Dual date slicers** allowing users to select any two custom time periods
- Side-by-side KPI comparison for Sales, Profit, and Quantity
- Powered by advanced DAX using `USERELATIONSHIP()` and inactive relationships

### 📉 Advanced DAX Measures
```dax
-- Quantity Sold (Period 2)
Quantity sold = CALCULATE(
    SUM('Fact Table'[Units Sold]),
    ALL('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date], 'Fact Table'[Date (dd/mm/yyyy)])
)

-- Net Sales (Period 2)
Sum of Net Sales = CALCULATE(
    SUM('Fact Table'[Net sales]),
    ALL('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date], 'Fact Table'[Date (dd/mm/yyyy)])
)

-- Total Profit (Period 2)
Total Profit = CALCULATE(
    SUM('Fact Table'[Profit]),
    All('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date], 'Fact Table'[Date (dd/mm/yyyy)])
)
```

### 🎛️ Interactive Features
- **Visual-level filters** for Product, Date, Customer ID, and Promotion Categories
- **Top/Bottom N analysis** for products
- **City-wise geographic breakdown**
- **Trend visualizations** across multiple time granularities
- **Discount analysis** by promotion category

---

## 📸 Screenshots

### Dashboard — Main Overview (City Map, KPIs, Trends & Promotions)
<p align="center">
  <img src="screenshots/dashboard_overview.png" alt="Dashboard Overview - Sales by City, Orders, Promotions, Profit vs Net Sales, Sales Trends" width="800"/>
</p>

### Dashboard — Period Comparison View (Bar Charts)
<p align="center">
  <img src="screenshots/dashboard_period_comparison.png" alt="Period Comparison Dashboard" width="800"/>
</p>

### Dashboard — KPI Comparison View (Horizontal Bars)
<p align="center">
  <img src="screenshots/dashboard_kpi_comparison.png" alt="KPI Comparison Dashboard" width="800"/>
</p>

### Data Model — Star Schema
<p align="center">
  <img src="screenshots/data_model.png" alt="Star Schema Data Model" width="800"/>
</p>

### Business Requirements
<p align="center">
  <img src="screenshots/business_requirements.png" alt="Business Requirements - 8 Key Questions" width="600"/>
</p>

### Dashboard — Top/Bottom 5 Products (Sales, Quantity & Profit)
<p align="center">
  <img src="screenshots/top_bottom_products.png" alt="Top and Bottom 5 Products by Sales, Quantity and Profit" width="800"/>
</p>

### Dashboard — Order Details Table (with Filters)
<p align="center">
  <img src="screenshots/order_details_table.png" alt="Order Details Table with Interactive Filters" width="800"/>
</p>

### Dashboard — Interactive Filters / Slicers
<p align="center">
  <img src="screenshots/filters_slicers.png" alt="Customer Name and Promotion Name Filter Slicers" width="800"/>
</p>

### DAX Measures
<p align="center">
  <img src="screenshots/dax_quantity_sold.png" alt="DAX Measure - Quantity Sold" width="600"/>
  <br/><br/>
  <img src="screenshots/dax_net_sales.png" alt="DAX Measure - Net Sales" width="600"/>
  <br/><br/>
  <img src="screenshots/dax_total_profit.png" alt="DAX Measure - Total Profit" width="600"/>
</p>

---

## 🚀 Getting Started

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Free)
- Microsoft Excel (to view dataset)

### How to Use
1. **Clone this repository**:
   ```bash
   git clone https://github.com/vivekgupta123741/powerbi-sales-data-analysis-dashboard.git
   ```
2. Open `dashboard/ElectroHub_Sales_Analysis.pbix` in Power BI Desktop
3. If prompted, update the data source path to point to `dataset/Store_Data.xlsx`
4. Explore the interactive dashboard!

---

## 📂 Project Structure

```
powerbi-sales-data-analysis-dashboard/
│
├── 📄 README.md                              # Project documentation (you are here)
├── 📄 .gitignore                             # Git ignore rules
├── 📄 LICENSE                                # MIT License
│
├── 📂 dataset/
│   └── Store_Data.xlsx                       # Source data (4 sheets, 3,500+ records)
│
├── 📂 dashboard/
│   └── ElectroHub_Sales_Analysis.pbix        # Power BI dashboard file
│
├── 📂 docs/
│   ├── Project_Requirements.pptx             # Business requirements & questions
│   └── Data_Model_Schema_Notes.pptx          # PK, FK, Cardinality documentation
│
├── 📂 screenshots/
│   ├── dashboard_overview.png                # Main dashboard (map, KPIs, trends)
│   ├── dashboard_period_comparison.png       # Period comparison view
│   ├── dashboard_kpi_comparison.png          # KPI metrics comparison
│   ├── top_bottom_products.png               # Top/Bottom 5 products analysis
│   ├── order_details_table.png               # Order details with filters
│   ├── filters_slicers.png                   # Customer & Promotion slicers
│   ├── data_model.png                        # Star schema diagram
│   ├── business_requirements.png             # Business requirements
│   ├── dax_quantity_sold.png                 # DAX measure screenshot
│   ├── dax_net_sales.png                     # DAX measure screenshot
│   └── dax_total_profit.png                  # DAX measure screenshot
│
└── 📂 resources/
    └── data_dictionary.md                    # Detailed column descriptions
```

---

## 📚 Lessons Learned

- **Star Schema Design**: Implemented proper dimensional modeling with fact and dimension tables for optimal query performance
- **Inactive Relationships**: Used `USERELATIONSHIP()` DAX function to leverage inactive relationships for period-over-period comparison — a real-world BI technique
- **Dual Date Tables**: Created two date tables to enable flexible user-driven period comparison
- **DAX Calculated Measures**: Built custom measures using `CALCULATE`, `ALL`, `SUM`, and `USERELATIONSHIP` for dynamic analysis
- **Data Modeling**: Established proper PK/FK relationships with correct cardinality (1:* and *:1)

---

## 🔮 Future Improvements

- [ ] Add **forecasting** using Power BI's built-in analytics
- [ ] Integrate **SQL Server** as the data source instead of Excel
- [ ] Build a **Customer Segmentation** analysis (RFM Analysis)
- [ ] Add **YoY/MoM growth rate** calculated measures
- [ ] Create a **mobile-optimized** dashboard layout
- [ ] Publish to **Power BI Service** for online access
- [ ] Add **Bookmarks & Drill-through** pages for detailed analysis

---

## 👤 Author

**Vivek Gupta**

- 🔗 GitHub: [@vivekgupta123741](https://github.com/vivekgupta123741)
- 💼 LinkedIn: [Connect with me](https://linkedin.com/in/YOUR-LINKEDIN-ID)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## ⭐ Support

If you found this project helpful, please consider giving it a ⭐ on GitHub!

---

<p align="center">
  <i>Built with ❤️ using Power BI | © 2024-2025 Vivek Gupta</i>
</p>
