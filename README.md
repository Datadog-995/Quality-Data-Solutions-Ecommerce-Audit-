

## 🧠 Tech Stack & Tools
* **Python Pandas:** High-performance data auditing, schema normalization, and row imputation.
* **Jupyter Notebooks / Google Colab:** Documented end-to-end reproducible Python code workflows.
* **Kaggle E-Commerce Datasets:** Used as a benchmark for complex, multi-variable retail data structures.

---
E-Commerce Automated Data Quality Pipeline
A Quality Data Solutions Project

📌 Project Overview
This repository contains a production-ready data cleaning and automated quality assurance pipeline built using Python and Pandas. The project sanitizes a raw, real-world e-commerce retail sales dataset by enforcing standardized schemas, repairing compromised text and missing entries, and generating standalone Data Quality Audit Flags to maintain reporting integrity.

This pipeline ensures that messy, transactional log files are perfectly formatted, reliable, and ready for ingestion into business intelligence (BI) live reporting dashboards or down-stream SQL warehouses.

(BEFORE) - SCREENSHOT ECOMMERCE DATASET MESSY DATA
<img width="725" height="360" alt="Screenshot 2026-07-09 at 7 21 45 PM" src="https://github.com/user-attachments/assets/4fb17886-e390-417e-ad92-dfaae8aa52c3" />

(AFTER) - SCREENSHOT ECOMMERCE DATASET CLEANED DATA   (FIT MOST COLUMNS IN SHOT, MORE COLUMNS ARE IN TOTAL FILE DOWNLOAD)
<img width="725" height="360" alt="Screenshot 2026-07-09 at 7 21 45 PM copy" src="https://github.com/user-attachments/assets/1ad7f07b-0151-4bbe-8680-06aa315405ef" />


🛠️ Data Quality Rules & Architecture
The script processes raw transactional records and systematically handles data anomalies based on strict governance rules:

1. Global Sanitization
Anomaly Handling: Identifies and completely strips out standalone textual placeholders (such as single dashes -) across the entire dataset without breaking legitimate internal codes (like ORD-10001 or SKU-1003).

2. Financial Record Sanitization (Price)
Format Alignment: Forces invalid text characters and missing values into perfectly clean, blank cells to maintain a strict numeric column profile.

Audit Tracking: Simultaneously maps rows with completely missing or non-numeric prices with an unknown flag in the adjacent Price_Audit_Flag column.

Accounting Verification: Flags pricing anomalies where the transaction value drops below zero as negative.

3. Inventory Validation (Quantity)
Format Alignment: Strips out accidental text words or blank values, leaving the core column purely numeric.

Missing Values: Identifies empty or corrupted fields and tracks them as unknown within the Quantity_Audit_Flag metric.

Inventory Control: Captures inventory anomalies where quantities are registered below zero (e.g., reverse or accidental entry values) and isolates them using a negative classification.

4. Temporal Standardization (Order Date)
Format Alignment: Converts fragmented date text strings into a unified MM-DD-YYYY datetime sequence.

Format Validation: Detects impossible calendar dates (e.g., 13/45/2026) or textual noise, completely blanks out the main cell, and registers an invalid state in the adjacent trans date audit column. Missing values are similarly designated as unknown.

🚀 Technical Stack
Language: Python 3.x

Libraries: Pandas, NumPy

Environment: Jupyter Notebooks / Google Colab

📊 Sample Visual Summary
Order ID	Order Date	trans date audit	Price	Price_Audit_Flag	Quantity	Quantity_Audit_Flag
ORD-10001	[Blank]	unknown	[Blank]	unknown	1.0	
ORD-10002	12-03-2025		24.64		5.0	
ORD-10005	[Blank]	invalid	175.03		1.0	
ORD-10034	02-21-2026		28.89		[Blank]	negative
⚙️ How to Run the Pipeline
Clone the repository:

Bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
Ensure you have the required dependencies installed:

Bash
pip install pandas numpy
Run the Jupyter Notebook or execute the consolidated transformation pipeline script to generate the fully optimized export asset: fully_cleaned_ecommerce_orders.csv.
