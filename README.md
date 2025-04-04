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
- Use time series models to forecast sales for the next 6 months.
<img width="373" alt="image" src="https://github.com/user-attachments/assets/62c330f3-5069-4d02-b880-25398a9e6aa4" />
- List the top 5 best-selling products.
<img width="445" alt="image" src="https://github.com/user-attachments/assets/0b6ee5ec-c1cf-4f96-9928-1d4e92cc0568" />
- Which weekday has the highest revenue?
📅 Thursday – with £1,973,015.73 in total sales.
- Predict sales for the next 3 months
<img width="332" alt="image" src="https://github.com/user-attachments/assets/151173a8-54e4-4523-b8f0-c15f70d79ab5" />
- Show monthly revenue trends
![image](https://github.com/user-attachments/assets/a97587db-3027-40f0-9c00-2b0345a9d79c)
- Dashboard:
![image](https://github.com/user-attachments/assets/efdbbdab-db1a-4c9c-b910-d3b29d9540a5)



## Future Work

- Instead of uploading dataset manually,  we can use connectors like PyMysql to inject data directly to verodat.
- Since Dashboards Generated is not interactive, I will be using connectors to send dataset to PowerBI to create interactive dashboards with KPI's, Descriptive analysis etc...
