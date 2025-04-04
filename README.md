# UK-sales-insights
End-to-end analytics pipeline using Verodat, GPT and Power BI
# 🧠 AI-Powered Retail Data Intelligence with Python, Verodat, GPT & Power BI

This project demonstrates an end-to-end data intelligence pipeline using Python for data cleaning, Verodat for schema modeling and LLM-based analytics, a custom GPT for natural language querying, and Power BI for real-time dashboarding.

---

## 📂 Dataset

Retail transaction-level invoice data containing:
- InvoiceNo, StockCode, Description, Quantity
- InvoiceDate, UnitPrice, CustomerID, Country

---

## 🧹 1. Data Cleaning with Python

Cleaned raw data using `pandas`:

- Removed `CustomerID = "Guest"`
- Converted `CustomerID` from float to integer
- Dropped duplicate rows
- Normalized `StockCode` conflicts (e.g., multiple descriptions/prices)
- Added derived fields: `TotalPrice`, `Year`, `Month`, `DayOfWeek`

> 📄 Final Output: `fact_sales.csv`

---

## 🔗 2. Injecting Data into Verodat using Connectors & AI Agents

- Used **Verodat SDK and AI agents** to upload cleaned datasets
- Promoted all datasets from design to staging to **Live** mode
- Assigned schema types (e.g., date, integer, category) before promoting to live

---

## 🧱 3. Data Normalization (Star Schema)

Split the dataset into 4 normalized tables:

| Table         | Keys                       | Description                      |
|---------------|----------------------------|----------------------------------|
| `dim_customer`| `CustomerID`               | Customer dimension               |
| `dim_product` | `StockCode`                | Product dimension                |
| `dim_date`    | `DateID` (derived)         | Date dimension                   |
| `fact_sales`  | `InvoiceNo`, `StockCode`   | Sales transactions (fact table)  |

Used Verodat’s **validation rules** with `LOOKUP_EXISTS()` to enforce FK–PK integrity across datasets.

---

## 🧠 4. Custom ChatGPT Integration

Built a **custom GPT** with:
- OpenAI API key
- Embedded schema and metadata
- Contextual instructions for business logic
(Note: The dataset must be uploaded twice once during design for METADATA and once in Live for actual data with outputs)
This enabled GPT to answer **natural language queries** like:

## Example Natural Language text
- Show monthly revenue trends
- What are the top 10 products by sales?
- Which weekday has the highest revenue?
- Predict sales for the next 3 months

## Future Work

- Instead of uploading dataset manually,  we can use connectors like PyMysql to inject data directly to verodat.
- Since Dashboards Generated is not interactive, I will be using connectors to send dataset to PowerBI to create interactive dashboards with KPI's, Descriptive analysis etc...
