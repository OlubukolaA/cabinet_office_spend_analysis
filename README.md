# Cabinet Office Spend Analysis of (Over £25,000) (Power BI)

An An end-to-end business intelligence solution analysing over **£2B** in public procurement and expenditure transactions from the UK Cabinet Office. This project
demonstrates advanced data , star-schema data modelling, custom fiscal time-intelligence, and executive dashboard design aligned with the **Microsoft PL-300: Power BI Data Analyst Certification** standards.

#
## Project Objective
To transform fragmented monthly government transparency records into actionable financial governance tool that provides a clear, interactive view of Cabinet Office expenditure, highlight major cost drivers, identify supplier concentration, and support transparency and financial governance.

## Data Architecture & Source
* **Primary Source**: UK Government Transparency Portal - [Cabinet Office Spend Data Collection](https://www.gov.uk/government/publications/cabinet-office-spend-data)
* **Dataset Scope**: 12 months of transactional records capturing all departmental outlays exceeding the £25,000 statutory publication threshold.
* **Core Attributes**: Transaction Date, Supplier Name, Expense Area, Financial Amount, and Narrative Description.
#
## Data Engineering & ETL Pipeline

### Automated Folder Ingestion
To mirror a scalable corporate data warehouse environment, I deployed a **Get Data From Folder** pipeline in Power Query. This ensures the ingestion engine automatically maps, combines, and transforms new monthly CSV inputs upon data refresh without requiring manual schema re-configurations.

### Power Query Transformations & Data Cleansing
* Enforced correct data types, handled missing data inputs, enforced appropriate numeric data typologies, and stripped transactional cents to optimize row processing memory.
* Referenced Dimension Modelling: Created independent Supplier and Category dimension tables by referencing the primary fact table, ensuring that downstream dimensions inherit up-to-date data cleansing transformations automatically.

### Custom UK Fiscal Calendar Table
Because the UK public sector operates on an explicit **April-to-March** accounting sequence rather than a standard calendar year, I developed a custom date dimension utilizing the following DAX framework to establish correct reporting boundaries:

*Note: To prevent alphabetical chart rendering errors, the MonthName visual column was explicitly mapped to sort by the underlying numeric FinancialMonth key.*

#

## The Star Schema Data Model
The semantic model follows a rigid Star Schema deployment utilising one-to-many (1:*) relationships to maintain peak cross-filtering:

* **Financial_Expenditure ➔ Supplier (1:*)**: Maps unique vendor dimensions down to transactional invoice entries, unlocking multi-tier contractor spend aggregations.
* **Financial_Expenditure ➔ Category (1:*)**: Links corporate procurement categories to line items to track internal operational expense area.
* **Financial_Expenditure ➔ Date_Table (1:*)**: Binds the custom fiscal timeline to the transactional registry to drive all downstream trend analysis and accounting period calculations.
! [] (Data_Model.png)

#

## Key DAX Calculation
### 1. Financial Run-Rate Measures

#

## 📊 Summary-to-Detail Dashboard Features

### Page 1: Spend Overview (Macro Visibility)
Provides an immediate, high-density diagnostic view of macro spending patterns. Features dynamic trend lines displaying monthly run-rates (highlighting seasonal procurement spikes in June and March), horizontal value ranking charts, and metric scorecard components tracking a **£2.07B** baseline outlay across **7,384** transactions.

### Page 2: Procurement Analysis (Commercial Concentrations)
Focuses heavily on market dominance and vendor exposure matrices. Incorporates interactive **Decomposition Tree** to dynamically drill from expense categories down to specific suppliers, paired with custom contract **Scatter Plots** that separate high-frequency operational vendors from low-volume strategic partners.

### Page 3: Transaction Insights (Volume vs. Value Risk)
Exposes the core risk divergence within government procurement structures. By evaluating the portfolio side-by-side, the visual layouts demonstrate that while low-tier operational transactions (<£100K) absorb over 75% of administrative invoice volume, a microscopic subset of hyper-value contracts (>£1M) controls a staggering 57.67% of total Cabinet Office funding outlays.

#
## Executive Insights & Strategic Impact
* Concentration Vulnerability: Identified severe budgetary dependence on isolated single-source entities, specifically within the *Infected Blood Compensation Authority (IBCA)* and the *Department for Work & Pensions (DWP)*.
* Fixed Overhead Constraints: Uncovered significant real estate cost pressures, proving that *Landlord Services* and fixed infrastructural assets form the largest ongoing monthly operational cash commitments.
* Operational Auditing: Delivers an automated, self-sanitizing "Million-Pound Club" ledger that strips away low-value processing noise, allowing regulatory auditors to immediately track high-risk milestone payments.

#

Files Included
Cabinet Office Spend Expenditure Over £25,000.pbix — full Power BI model
Dashboard Screenshots — visual overview of insights
README.md — project documentation

