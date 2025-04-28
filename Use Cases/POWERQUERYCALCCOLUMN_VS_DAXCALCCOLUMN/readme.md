# Data Model Description

Se ci trovassimo nella situazione di dover creare una colonna calcolata che si basa sui valori di una tabella in PowerBI potremmo farlo in due modi differenti. Creando una colonna calcolata in Power Query o creando una colonna calcolata in DAX.

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