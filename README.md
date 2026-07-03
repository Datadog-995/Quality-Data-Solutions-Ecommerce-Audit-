# QualityData Solutions: E-Commerce Data Integrity & Quality Audit Pipeline

An end-to-end data engineering and quality assurance pipeline built in Python to audit, clean, and standardize transactional e-commerce datasets. This project demonstrates how systematic data scrubbing eliminates reporting anomalies, restores corrupted entries, and prepares messy raw data for downstream business intelligence and analytics dashboards.

## 📌 Business Problem & Impact
Unstandardized text, missing transactional values, and corrupted data formats introduce significant errors into financial reporting and inventory forecasting. For instance:
* **Negative Prices:** Distort gross revenue metrics and average order value (AOV) calculations.
* **Missing Unit Prices:** Cause incomplete transaction records, skewing total sales counts.
* **Corrupted Date Formats:** Break database ingestion scripts and time-series forecasting models.

**The Solution:** This automated pipeline flags formatting anomalies without throwing away valuable transaction history, programmatically repairs missing numeric metrics using relational SKU mapping, and enforces strict structural compliance across the entire dataset.

---

## 🛠️ Tech Stack & Tools
* **Language:** Python 3
* **Libraries:** Pandas, NumPy, Regular Expressions (`re`)
* **Environment:** Google Colab / Jupyter Notebooks

---

## ⚙️ Core Logic & Pipeline Architecture

The pipeline processes raw transactional records through five dedicated stages:

### 1. Structural Workspace Cleanup
* Identifies and drops empty metadata placeholders, dead workspace tracking blocks, and redundant audit columns (`Price_Audit_Flag`, `Quantity_Audit_Flag`, `Data Quality Status`, etc.) to optimize memory utilization and data clarity.

### 2. Relational Price Restoration & Anomaly Correction
* **Missing Value Recovery:** Dynamically maps missing product unit prices by grouping matching `SKU` items and backfilling empty fields using the first known valid pricing record.
* **Sign Correction:** Detects structural sign errors (negative prices) and programmatically flips them to clean, positive absolute values (`.abs()`).
* **Audit Lineage:** Injects a dedicated `Price Audit Column` to preserve data lineage, tracking exactly which records were `Valid`, `Missing Price - Restored via SKU`, or `Negative Price - Converted to Positive`.

### 3. Temporal Validation (Date Auditing)
* Parses order timelines using comprehensive conditional logic (`np.select`).
* Isolates corrupted text strings (e.g., `13/45/2026`) from completely empty fields, successfully binning them into explicit `Invalid Date String` or `Missing Date Entry` categories within an adjacent `Order Date Audit Flag` column.

### 4. Categorical & Text Standardization
* Strips leading/trailing whitespaces and converts text columns (like `Order Status`) into standard lowercase strings to eliminate duplicate categorical categories (e.g., matching "unfulfilled" with "Unfulfilled").
* Replaces irregular text variations in payment processors (e.g., standardizing "Pay Pal" to "PayPal").

### 5. Data Integrity Constraints
* Enforces strict typing rules by casting the `Quantity` field into clean, integer formats.
* Utilizes Regex compilation (`r'^[\w\.-]+@[\w\.-]+\.\w+$'`) to run boolean validation tracking on `Customer Email` structures.
* Drops exact duplicate records to ensure absolute dataset uniqueness.

---

## 📊 Sample Output Schema
After running the pipeline, the final optimized DataFrame retains the following verified structure:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Order ID` | Object / String | Unique alphanumeric transaction identifier |
| `SKU` | Object / String | Unique product stock keeping unit |
| `Product Name` | Object / String | Cleansed title of the listed e-commerce item |
| `Category` | Object / String | Standardized retail department category |
| `Price` | Float | Audited, positive unit cost |
| `Price Audit Column` | Object / String | Audit trail tracker (`Valid`, `Restored via SKU`, etc.) |
| `Quantity` | Integer | Cleaned transactional item count |
| `Payment Method` | Object / String | Standardized processing method (e.g., `PayPal`) |
| `Order Status` | Object / String | Lowercase structural status record |
| `Order Date` | Object / String | Raw transaction date string |
| `Order Date Audit Flag`| Object / String | Quality assessment flag (`Valid`, `Invalid Date String`, etc.) |
| `Customer Email` | Object / String | User communication address |
| `Email_Valid` | Boolean | Regex confirmation of proper email layout (`True`/`False`) |

---

## 🚀 How To Run
1. Clone this repository:
   ```bash
   # QualityData Solutions: E-Commerce Data Integrity & Quality Audit Pipeline

An end-to-end data engineering and quality assurance pipeline built in Python to audit, clean, and standardize transactional e-commerce datasets. This project demonstrates how systematic data scrubbing eliminates reporting anomalies, restores corrupted entries, and prepares messy raw data for downstream business intelligence and analytics dashboards.

## 📌 Business Problem & Impact
Unstandardized text, missing transactional values, and corrupted data formats introduce significant errors into financial reporting and inventory forecasting. For instance:
* **Negative Prices:** Distort gross revenue metrics and average order value (AOV) calculations.
* **Missing Unit Prices:** Cause incomplete transaction records, skewing total sales counts.
* **Corrupted Date Formats:** Break database ingestion scripts and time-series forecasting models.

**The Solution:** This automated pipeline flags formatting anomalies without throwing away valuable transaction history, programmatically repairs missing numeric metrics using relational SKU mapping, and enforces strict structural compliance across the entire dataset.

---

## 🛠️ Tech Stack & Tools
* **Language:** Python 3
* **Libraries:** Pandas, NumPy, Regular Expressions (`re`)
* **Environment:** Google Colab / Jupyter Notebooks

---

## ⚙️ Core Logic & Pipeline Architecture

The pipeline processes raw transactional records through five dedicated stages:

### 1. Structural Workspace Cleanup
* Identifies and drops empty metadata placeholders, dead workspace tracking blocks, and redundant audit columns (`Price_Audit_Flag`, `Quantity_Audit_Flag`, `Data Quality Status`, etc.) to optimize memory utilization and data clarity.

### 2. Relational Price Restoration & Anomaly Correction
* **Missing Value Recovery:** Dynamically maps missing product unit prices by grouping matching `SKU` items and backfilling empty fields using the first known valid pricing record.
* **Sign Correction:** Detects structural sign errors (negative prices) and programmatically flips them to clean, positive absolute values (`.abs()`).
* **Audit Lineage:** Injects a dedicated `Price Audit Column` to preserve data lineage, tracking exactly which records were `Valid`, `Missing Price - Restored via SKU`, or `Negative Price - Converted to Positive`.

### 3. Temporal Validation (Date Auditing)
* Parses order timelines using comprehensive conditional logic (`np.select`).
* Isolates corrupted text strings (e.g., `13/45/2026`) from completely empty fields, successfully binning them into explicit `Invalid Date String` or `Missing Date Entry` categories within an adjacent `Order Date Audit Flag` column.

### 4. Categorical & Text Standardization
* Strips leading/trailing whitespaces and converts text columns (like `Order Status`) into standard lowercase strings to eliminate duplicate categorical categories (e.g., matching "unfulfilled" with "Unfulfilled").
* Replaces irregular text variations in payment processors (e.g., standardizing "Pay Pal" to "PayPal").

### 5. Data Integrity Constraints
* Enforces strict typing rules by casting the `Quantity` field into clean, integer formats.
* Utilizes Regex compilation (`r'^[\w\.-]+@[\w\.-]+\.\w+$'`) to run boolean validation tracking on `Customer Email` structures.
* Drops exact duplicate records to ensure absolute dataset uniqueness.

---

## 📊 Sample Output Schema
After running the pipeline, the final optimized DataFrame retains the following verified structure:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Order ID` | Object / String | Unique alphanumeric transaction identifier |
| `SKU` | Object / String | Unique product stock keeping unit |
| `Product Name` | Object / String | Cleansed title of the listed e-commerce item |
| `Category` | Object / String | Standardized retail department category |
| `Price` | Float | Audited, positive unit cost |
| `Price Audit Column` | Object / String | Audit trail tracker (`Valid`, `Restored via SKU`, etc.) |
| `Quantity` | Integer | Cleaned transactional item count |
| `Payment Method` | Object / String | Standardized processing method (e.g., `PayPal`) |
| `Order Status` | Object / String | Lowercase structural status record |
| `Order Date` | Object / String | Raw transaction date string |
| `Order Date Audit Flag`| Object / String | Quality assessment flag (`Valid`, `Invalid Date String`, etc.) |
| `Customer Email` | Object / String | User communication address |
| `Email_Valid` | Boolean | Regex confirmation of proper email layout (`True`/`False`) |

---

## 🚀 How To Run
1. Clone this repository:
   ```bash
   git clone [https://github.com/Datadog-995/Quality-Data-Solutions-Ecommerce-Audit-.git](https://github.com/Datadog-995/Quality-Data-Solutions-Ecommerce-Audit-.git)
