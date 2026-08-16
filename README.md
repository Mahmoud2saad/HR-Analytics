# HR Analytics Dashboard | Power BI End-to-End BI Solution

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

An end-to-end Business Intelligence project built in **Power BI** that transforms raw, messy HR data into a fully interactive analytics suite — covering attrition, attendance, performance, and workforce demographics. Built to mirror a real workplace HR analytics engagement, from data cleaning through to executive-ready dashboards.

**🔗 [Live Report / Screenshots](#-dashboard-previews)** · **📁 [Dataset](./Dataset)** · **📊 [.pbix File](./HR_Analytics_Dashboard.pbix)**

---

## 📌 Project Summary

| | |
|---|---|
| **Objective** | Give HR leadership a single source of truth to diagnose *why* employees leave, *who* is at risk, and *where* attendance/performance issues concentrate |
| **Data Sources** | 4 raw HR tables (General, Employee Survey, Manager Survey, In/Out Time logs) — ~4,400 rows, 40+ fields |
| **Deliverables** | 3-page interactive Power BI dashboard, cleaned data model, DAX measure library, PPTX executive summary |
| **My Role** | Solo — data cleaning, modeling, DAX, UX design, and insight write-up |
| **Tools** | Power BI Desktop, Power Query (M), DAX, Star Schema data modeling |

---

## 🎯 Business Problem & Objectives

HR held attrition, satisfaction, and attendance data across disconnected spreadsheets with no unified reporting layer. Leadership couldn't answer basic questions quickly: *Which department is bleeding talent? Is overtime driving attrition? Are satisfaction scores tied to commute distance?*

This dashboard was built to:
- Surface attrition patterns by department, age group, and gender
- Monitor attendance, overtime, and late-arrival trends over time
- Quantify the link between satisfaction/performance and retention
- Flag high-risk employee segments before they become attrition statistics
- Give HR a self-service tool instead of ad-hoc spreadsheet pulls

---

## 🛠️ Tools & Technical Stack

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard development, DAX modeling, visualization |
| **Power Query (M)** | Data cleaning, unpivoting, merging, transformation |
| **DAX** | KPI measures, calculated columns, time intelligence |
| **Data Modeling** | Star schema, relationship design, cardinality management |
| **Git/GitHub** | Version control & portfolio hosting |

---

## 📂 Repository Structure

```
HR-Analytics-Dashboard/
│
├── Dataset/
│   ├── raw_data/                     # Original, unprocessed HR exports
│   └── cleaned_data/                 # Post Power Query transformation
│
├── Presentation/
│   └── HR_Analytics_Presentation.pptx
│
├── Screenshots/
│   ├── overview-dashboard.png
│   ├── employees-dashboard.png
│   ├── attendance-dashboard.png
│   └── data-model.png
│
├── HR_Analytics_Dashboard.pbix       # Full Power BI report
└── README.md
```

---

## 🧹 Data Cleaning & Transformation (Power Query)

Raw HR exports arrived across four disconnected tables with inconsistent encoding, missing values, and a wide/unpivoted time-log format. Key transformations:

**1. Employee Survey Data**
- Decoded numeric satisfaction codes (Environment, Job, Work-Life Balance) into readable labels
- Imputed missing ratings with the **median (3)** rather than the mean, to avoid distorting the ordinal 1–4 scale with outlier sensitivity

**2. General Employee Data**
- Decoded Education codes into readable categories
- Dropped constant-value columns (`EmployeeCount`, `Over18`, `StandardHours`) — zero analytical value, pure noise
- Imputed missing values in `NumCompaniesWorked` (median = 2) and `TotalWorkingYears` (median = 10)
- Engineered new fields: **Age Group**, **Distance Group**, and a **Distance Sort key** for correct visual ordering

**3. In-Time / Out-Time Logs**
- **Unpivoted** both wide-format tables (one column per date → one row per employee-date) to enable time-series analysis and relationship modeling
- Standardized null timestamps to a sentinel date (`01-01-1900`) to preserve row integrity without breaking joins
- Built a unified **Attendance fact table** by merging In/Out logs, then calculated **daily working hours per employee**

**4. Manager Survey Data**
- Decoded Job Involvement and Performance Rating codes into readable categories

> **Why this matters:** ~30% of the total build time went into this stage. Clean, well-typed, properly-shaped data is what makes the DAX layer fast and the visuals trustworthy — this is the part of BI work that doesn't show up in screenshots but determines whether the dashboard is actually usable.

---

## 🧠 Data Modeling

Designed a **star schema** with `General Data` as the central fact/dimension hub, connected to Survey and Attendance tables via `EmployeeID` using one-to-many relationships. A dedicated **Measures Table** (no data, DAX only) keeps all calculations organized and separate from raw fields.

**Why star schema over a flat/wide table:**
- Faster query performance — Power BI's VertiPaq engine is optimized for star schemas
- Simpler, more predictable filter propagation across visuals
- Easier to maintain and extend as new HR data sources are added
- Keeps DAX measures simple by avoiding ambiguous relationship paths

📷 *See [`Screenshots/data-model.png`](./Screenshots/data-model.png)*

---

## 📊 DAX Measures & KPI Library

Built a reusable measure library covering core HR KPIs, including:

```dax
Attrition Rate = 
DIVIDE(
    [Attrition Count],
    [Total Employees],
    0
)

Attendance Rate = 
DIVIDE(
    [Days Present],
    [Total Working Days],
    0
)

Average Working Hours = 
AVERAGEX(
    Attendance,
    Attendance[WorkingHours]
)
```

Full measure set: `Total Employees`, `Attrition Count`, `Attrition Rate`, `Average Satisfaction`, `Average Performance Rating`, `Average Working Hours`, `Attendance Rate`, `Overtime Rate`, `Late Arrival %`, `Average Income`, `Average Years at Company`.

---

## 📈 Dashboard Pages

### 🏠 1. Overview Dashboard
**Purpose:** Executive-level snapshot of attrition, satisfaction, performance, and attendance.

**KPIs:** Total Employees · Attrition Count · Avg. Job Satisfaction · Avg. Performance Rating · Avg. Working Hours

**Visuals:** Attrition by Department / Gender / Age Group · Avg. Satisfaction by Department · Avg. Performance by Department · Working Hours Trend · Recent Attrition Table

**Key Insights:**
- The **Human Resources department has the highest attrition rate** of any department
- **Younger employees (18–25 age group) leave at a disproportionately higher rate**
- Satisfaction and performance scores show only modest variation across departments — attrition is not purely a satisfaction problem
- Working hours fluctuate meaningfully across the year, suggesting seasonal workload spikes

📷 `Screenshots/overview-dashboard.png`

---

### 👥 2. Employees Dashboard
**Purpose:** Workforce demographics, compensation, and distribution analysis.

**KPIs:** Avg. Age · Avg. Income · Avg. Years at Company · Avg. Salary Hike · Avg. Training

**Visuals:** Distribution by Job Role · Age Distribution · Income by Job Level · Gender Distribution · Years at Company by Department · Marital Status · Education Field · Satisfaction by Distance Group · Satisfaction by Job Level & Department

**Key Insights:**
- The **26–35 age group** makes up the largest share of the workforce
- **Research Scientist** and **Sales Executive** are the dominant job roles by headcount
- Income scales clearly with job level, as expected — but salary hike % doesn't always follow the same pattern
- **Employees with longer commutes report lower satisfaction**, a signal worth investigating for retention risk

📷 `Screenshots/employees-dashboard.png`

---

### ⏰ 3. Attendance Dashboard
**Purpose:** Tracks attendance behavior, overtime, and lateness patterns.

**KPIs:** Avg. Working Hours · Attendance Rate · Avg. Absent Days · Late Arrival % · Overtime Rate

**Visuals:** Absent Days by Job Role · Late Arrival Trend · Absent Days by Gender · Overtime Days by Job Role · Overtime by Gender · Attendance Details Table

**Key Insights:**
- A small subset of job roles account for a disproportionate share of overtime hours
- Attendance behavior differs slightly by gender, though the gap is narrow
- Late arrivals show clear month-to-month fluctuation rather than being evenly distributed
- Certain job roles have a **noticeably higher absence rate**, worth cross-referencing against the attrition data

📷 `Screenshots/attendance-dashboard.png`

---

## 🎨 UI/UX Design Approach

Designed with a modern corporate aesthetic rather than default Power BI theming:
- Custom sidebar navigation with interactive page-switching buttons
- Consistent color palette and modern KPI cards
- Responsive layout with clear visual hierarchy to guide the eye toward the most important metrics first
- Prioritized readability and narrative flow over visual density — each page tells one story, not ten

---

## 🚀 Key Highlights

- ✅ **Full BI lifecycle** — raw data → cleaning → modeling → DAX → dashboard → business insight
- ✅ **Advanced Power Query** — unpivoting, table merges, null handling, calculated columns
- ✅ **Star schema data model** optimized for performance and maintainability
- ✅ **11+ custom DAX measures** covering attrition, attendance, and performance KPIs
- ✅ **3 fully interactive dashboard pages** with cross-filtering and drill-through
- ✅ **Actionable business insights**, not just charts — each page ends in a "so what"

---

## 📌 Conclusion & Business Impact

This project simulates a real HR analytics engagement: starting from fragmented, uncleaned data and ending with a self-service reporting tool that lets HR leadership:

- Identify and prioritize departments/roles at highest attrition risk
- Investigate the link between commute distance, satisfaction, and retention
- Monitor overtime and attendance trends to flag burnout risk early
- Move from reactive, spreadsheet-based reporting to proactive, data-driven HR decisions

---

## 👨‍💻 Author

**Mahmoud Saad**
Aspiring Data Engineer / BI Developer — focused on data analytics, dashboard development, and end-to-end business intelligence solutions.

📫 [LinkedIn](https://www.linkedin.com/in/mahmoud-saad0/) · [Github](https://github.com/Mahmoud2saad) · [Email](Mahmoud0Saad@outlook.com)


---

⭐ **If you found this project useful, consider giving the repository a star.**
