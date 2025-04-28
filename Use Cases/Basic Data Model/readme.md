# Data Model Description

This document describes the **Power BI data model** composed of four dimension tables and one fact table, designed for comprehensive sales analysis across time, geography, and product categories. The structure supports advanced time intelligence with a dedicated **retail calendar** for weekly-based reporting.

---

## Model Tables

### 1. `daily_sales.csv` (Fact Table: Daily Sales)

This table captures **daily sales transactions** across stores, products, and dates.

**Columns:**
- `ProductID` (FK) – Identifier of the sold product
- `Date` (FK) – Date of the transaction
- `SalesVolume` – Number of units sold
- `SalesValue` – Total sales value (including random variation between 5% and 25%)
- `StoreCode` (FK) – Store where the sale occurred
- `StoreWarehouse` (FK) – Store used as a warehouse (matches `StoreCode` 80% of the time)
- `Currency` – Transaction currency (EUR, USD, GBP)

---

### 2. `products.csv` (Dimension Table: Product)

Contains the **product catalog** for items available in the stores.

**Columns:**
- `ProductID` (PK) – Unique product identifier
- `ProductName` – Realistic product name
- `Category` – Product category (e.g., Electronics, Furniture, Toys, Clothing, Books)
- `Type` – Specific product type
- `Price` – Unit selling price
- `Stock` – Available inventory
- `LeadTime` – Procurement time in days
- `ManagedBy` – Business unit responsible (IT, EU, etc.)
- `Brand` – Product brand
- `Description` – Marketing description

---

### 3. `calendar_retail.csv` (Dimension Table: Calendar - Retail 4-4-5)

This table defines a **Retail 4-4-5 Calendar**, structured specifically for reporting across consistent weeks, months, and semesters. It is widely used in the retail industry to align reporting periods based on business cycles rather than fixed calendar months.

**Columns:**
- `Date` (PK) – Calendar date
- `RetailDayOfYear` – Day number within the retail year
- `RetailWeek` – Week number (1–52/53)
- `RetailMonth` – Retail month (1–12, grouped as 4-4-5 weeks per quarter)
- `RetailSemester` – Semester within the retail year (1 or 2)
- `RetailYear` – Year based on retail calendar
- `RetailMonthEnd` – Last day of the corresponding retail month
- `RetailWeekEnd` – Last day of the corresponding retail week
- `RetailSemesterEnd` – Last day of the corresponding semester
- `IsWeekend` – Flag for Saturdays (typical retail weekend day)
- `RetailYearStartPrev` – Start date of the previous retail year
- `MonthName` – Full name of the month
- `MonthAbbr` – Abbreviated name of the month

**Why Retail Calendar Instead of Fiscal Calendar?**  
Unlike traditional **fiscal calendars** that follow standard calendar months or arbitrary quarterly splits, the **retail calendar** organizes time into consistent 4-week, 4-week, 5-week months across each quarter. This allows for more balanced **period-over-period analysis**, where each period contains a comparable number of weekdays and weekends, crucial in retail where sales performance varies significantly between weekdays and weekends.

---

### 4. `stores.csv` (Dimension Table: Stores)

Contains the geographical and structural details of each retail store.

**Columns:**
- `StoreCode` (PK) – Unique store identifier
- `StoreName` – Name of the store
- `City` – Store location
- `Latitude` – Latitude for geo-visualizations
- `Longitude` – Longitude for geo-visualizations
- `Area` – Geographical macro area (North, Center, South)

---

## Model Relationships

- `daily_sales.csv` → `products.csv` via `ProductID`
- `daily_sales.csv` → `calendar_retail.csv` via `Date`
- `daily_sales.csv` → `stores.csv` via `StoreCode` and `StoreWarehouse`

---

This data model enables detailed and flexible analysis of sales trends, product performance, store comparisons, and retail time-based analytics using Power BI.