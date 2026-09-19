# Commercial Fit-Out & Construction Analytics | BI Case Study

An end-to-end business intelligence and data analytics system analyzing financial performance, cost structures, and operational delays across capital projects and commercial fit-outs.

This project processes transactional contract logs (valued at **135M AED**), structuring raw records into an enterprise **Star Schema**, relational **SQL** database, and a dynamic two-page **Power BI Executive Dashboard**.

---

## 📌 Case Study Overview & Key Findings

* **Total Project Volume Analyzed:** 135.0M AED across major commercial and residential developments.
* **Overall Gross Profit:** 43.0M AED (~32.2% Gross Margin).
* **Schedule Deviations:** Average completion variance of +8.0 days per project.
* **Core Business Finding:** Identified that cost overruns were heavily concentrated in commercial plaza projects driven by subcontractor expenses, while residential developments were primarily subject to material cost variances. Correlation analysis confirmed a clear drop in gross margin as project delay surpassed 15 days.

---

## 🏗️ Technical Pipeline

Raw Operational Logs (CSV / Excel)
         │
         ▼
Python / Pandas Pipeline (Cleaning, Null Imputation, Schema Standardization)
         │
         ▼
Relational Database (SQLite / 3NF Normalized Schema & Constraints)
         │
         ▼
Power BI Data Engine (Star Schema, Relational Integrity, Dynamic DAX Measures)
         │
         ▼
Interactive Dashboards (Executive Overview & Operational Diagnostics)

---

## 🛠️ Tech Stack

* **Data Cleaning & Pipeline:** Python (Pandas, NumPy)
* **Data Modeling & Storage:** SQL (SQLite, 3NF Normalization, Foreign Key Cardinality)
* **Business Intelligence:** Power BI Desktop
* **Calculations & Analytics:** DAX (`DIVIDE`, `CALCULATE`, `DISTINCTCOUNT`, Dynamic Margin & Variance Formulas)

---

## 📊 Data Model (Star Schema)

The data model connects normalized entities via one-to-many relationships:

* **Fact Table:**
  * `clean_projects_financials`: Tracks contract values, actual total costs, direct material/labor/subcontractor expenses, and completion delays.
* **Dimension Tables:**
  * `clean_clients`: Client categorizations and prime geographic locations.
  * `clean_lead_sources`: Inbound acquisition channels.
  * `clean_maintenance`: Annual maintenance contracts, project IDs, fees, and renewal states.
* **Measure Repository (`_Measures`):** Decoupled DAX business metrics computed dynamically across report filters.

---

## 📈 Dashboard Architecture

### Page 1: Executive Operations & Financial Overview
* **KPI Header Cards:** High-level executive tracking of Total Revenue, Gross Profit, Gross Margin %, and Average Schedule Delay.
* **Budget vs. Actual Variance:** Clustered column visualization comparing baseline budget estimates directly against realized expenditures per project type.
* **Revenue Contribution:** Donut chart evaluating revenue concentration across service lines.
* **Interactive Slicers:** Dynamic filtering by location and client segment to evaluate localized profitability.

### Page 2: Cost Slippage & Contractor Diagnostics
* **Delay vs. Margin Correlation (Scatter Plot):** Analyzes project delays against realized gross margins to detect thresholds of margin erosion.
* **100% Stacked Cost Composition:** Proportional expense distribution highlighting variance between subcontractor-heavy vs. material-heavy project categories.
* **Underperforming Contract Audit (Table):** Ranked ledger sorting low-margin and loss-making contracts for audit.

---

## 📐 Key DAX Measures


// Total Contract Volume
Total Revenue = SUM(clean_projects_financials[contract_value_aed])

// Realized Expenditure
Total Actual Cost = SUM(clean_projects_financials[actual_total_cost_aed])

// Gross Profit
Gross Profit = [Total Revenue] - [Total Actual Cost]

// Gross Margin Percentage
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)

// Average Delay
Avg Delay Days = AVERAGE(clean_projects_financials[schedule_delay_days_filled])

// AMC Conversion Rate %
AMC Conversion Rate % = 
DIVIDE(
    DISTINCTCOUNT(clean_maintenance[project_id]),
    CALCULATE(
        DISTINCTCOUNT(clean_projects_financials[project_id]), 
        clean_projects_financials[status] = "Completed"
    ),
    0
)

##How to Run Locally
Clone the repository:

//Bash
git clone [https://github.com/Adil-Ahamed2004/Capital-Project-Financial-Analytics.git](https://github.com/Adil-Ahamed2004/Capital-Project-Financial-Analytics.git)
cd Capital-Project-Financial-Analytics

//Open the Power BI File:

Launch grefton_executive_dashboard.pbix in Power BI Desktop to interact with the dashboards.

//Review Pipeline:

Explore data transformation scripts in notebooks/ and relational SQL queries in sql/.
