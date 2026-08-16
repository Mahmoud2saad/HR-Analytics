# HR Analytics Dashboard using Power BI

## 📌 Project Overview

This project is an end-to-end **HR Analytics Solution** developed using **Power BI**, **Power Query**, and **DAX** to analyze employee behavior, workforce trends, attrition, attendance, satisfaction, and performance.

The goal of this project is to transform raw HR datasets into meaningful business insights that support data-driven HR decision-making.

The solution covers the complete Business Intelligence workflow:

* Data Cleaning
* Data Transformation
* Data Modeling
* DAX Calculations
* Dashboard Design
* Business Insights Extraction

---

# 🎯 Business Objectives

The dashboard was designed to help HR teams:

* Analyze employee attrition patterns
* Monitor employee attendance and overtime
* Measure employee satisfaction and performance
* Identify high-risk employee groups
* Understand workforce demographics
* Support HR strategic decision-making using data

---

# 🛠️ Tools & Technologies Used

| Tool          | Purpose                                 |
| ------------- | --------------------------------------- |
| Power BI      | Dashboard development & visualization   |
| Power Query   | Data cleaning & transformation          |
| DAX           | KPI calculations & measures             |
| Data Modeling | Relationship management                 |
| GitHub        | Project versioning & portfolio showcase |

---

# 📂 Project Structure

```bash
HR-Analytics-Dashboard/
│
├── Dataset/
│   ├── raw_data/
│   └── cleaned_data/
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
├── HR_Analytics_Dashboard.pbix
└── README.md
```

---

# 🧹 Data Cleaning & Transformation

## 1️⃣ Employee Survey Data

### Transformations:

* Decoded Environment Satisfaction values into readable text categories
* Decoded Job Satisfaction values into readable text categories
* Decoded Work Life Balance values into readable text categories
* Replaced missing values using the median value (3)

### Why Median?

The median was used instead of the mean because it is less affected by outliers and better preserves the natural distribution of ordinal survey ratings.

---

## 2️⃣ General Data

### Transformations:

* Decoded Education values into readable categories
* Removed Employee Count column because it contained a constant value for all employees
* Replaced missing values in Number of Companies Worked using the median value (2)
* Replaced missing values in Total Working Years using the median value (10)
* Removed Over18 column because all employees had the same value
* Removed Standard Hours column because all employees had the same value (8)
* Added Age Group column
* Added Distance Group column
* Added Distance Sort column for proper visual sorting

---

## 3️⃣ In Time & Out Time Tables

### Transformations:

* Unpivoted both tables
* Converted dates from columns into rows
* Replaced null date values with:

```text
01-01-1900 12:00:00 AM
```

* Added a separate Date column

### Why Unpivoting?

Unpivoting transformed the data into a normalized structure suitable for:

* Time-series analysis
* Filtering
* Relationship modeling
* Attendance calculations

---

## 4️⃣ Manager Survey Data

### Transformations:

* Decoded Job Involvement values into readable text categories
* Decoded Performance Rating values into readable text categories

---

## 5️⃣ Attendance Table Creation

A new Attendance table was created by merging:

* In Time table
* Out Time table

### The table includes:

* Employee ID
* Date
* In Time
* Out Time
* Working Hours

### Additional Calculations:

* Working hours were calculated per employee per day.

---

# 🧠 Data Modeling

The project follows a **Star-Like Schema** design.

## Model Design:

* General Data acts as the central table
* Survey and attendance tables are connected using EmployeeID
* One-to-Many relationships were used for optimized filtering and aggregation
* A dedicated Measures Table was created to organize all DAX calculations

### Why Star Schema?

* Better Power BI performance
* Easier maintenance
* Simpler relationships
* More efficient DAX calculations
* Cleaner and scalable architecture

---

# 📊 DAX Measures & KPIs

The project includes several DAX measures such as:

* Total Employees
* Attrition Count
* Attrition Rate
* Average Satisfaction
* Average Performance Rating
* Average Working Hours
* Attendance Rate
* Overtime Rate
* Late Arrival Percentage
* Average Income
* Average Years at Company

---

# 📈 Dashboard Pages

---

# 🏠 1. Overview Dashboard

## Purpose

Provides a high-level overview of employee attrition, satisfaction, performance, and attendance trends.

## KPIs Included

* Total Employees
* Attrition Count
* Average Job Satisfaction
* Average Performance Rating
* Average Working Hours

## Visuals Included

* Attrition by Department
* Attrition by Gender
* Attrition by Age Group
* Average Satisfaction by Department
* Average Performance Rating by Department
* Average Working Hours Trend
* Recent Attrition Employees Table

## Key Insights

* Human Resources department has the highest attrition rate.
* Younger employees are more likely to leave the company.
* Satisfaction and performance vary slightly across departments.
* Working hours fluctuate throughout the year.

---

## 📷 Dashboard Preview

![Overview Dashboard](Screenshots/Overview-Dashboard.png)

---

# 👥 2. Employees Dashboard

## Purpose

Analyzes workforce demographics, salaries, education, and employee distribution.

## KPIs Included

* Average Age
* Average Income
* Average Years at Company
* Average Salary Hike
* Average Training

## Visuals Included

* Employee Distribution by Job Role
* Age Distribution
* Income by Job Level
* Gender Distribution
* Years at Company by Department
* Marital Status Distribution
* Education Field Distribution
* Satisfaction by Distance Group
* Satisfaction by Job Level and Department

## Key Insights

* Most employees belong to the 26–35 age group.
* Research Scientist and Sales Executive are dominant job roles.
* Higher job levels correspond to higher salaries.
* Satisfaction levels vary based on commuting distance.

---

## 📷 Dashboard Preview

![Employees Dashboard](Screenshots/Employees-Dashboard.png)

---

# ⏰ 3. Attendance Dashboard

## Purpose

Tracks employee attendance behavior, overtime, lateness, and absence trends.

## KPIs Included

* Average Working Hours
* Attendance Rate
* Average Absent Days
* Late Arrivals Percentage
* Overtime Rate

## Visuals Included

* Total Absent Days by Job Role
* Late Arrivals Trend
* Absent Days by Gender
* Overtime Days by Job Role
* Overtime by Gender
* Attendance Details Table

## Key Insights

* Some job roles experience significantly more overtime.
* Attendance behavior varies slightly between genders.
* Late arrivals fluctuate across different months.
* Certain job roles have noticeably higher absence rates.

---

## 📷 Dashboard Preview

![Attendance Dashboard](Screenshots/Attendance-Dashboard.png)

---

# 🧩 Data Model

## 📷 Data Model Preview

![Data Model](Screenshots/Data-Model.png)

---

# 🎨 UI / UX Design

The dashboards were designed using a modern corporate UI style.

## Design Features

* Custom sidebar navigation
* Interactive buttons
* Consistent color palette
* Modern KPI cards
* Responsive layout
* Clean visual hierarchy

The main focus was improving:

* Readability
* User experience
* Dashboard navigation
* Business storytelling

---

# 🚀 Project Highlights

✅ End-to-End BI Workflow

✅ Advanced Power Query Transformations

✅ DAX Calculations & KPIs

✅ Star Schema Data Modeling

✅ Interactive Dashboard Design

✅ HR Business Insights Extraction

---

# 📌 Conclusion

This project demonstrates a complete Business Intelligence workflow starting from raw HR data all the way to interactive dashboards and business insights.

The solution enables HR teams to:

* Reduce attrition
* Improve employee satisfaction
* Monitor attendance patterns
* Understand workforce behavior
* Make data-driven decisions

---

# 👨‍💻 Author

**Mina Morkos**

Aspiring Data Engineer / BI Developer passionate about data analytics, dashboard development, and business intelligence solutions.

---

# ⭐ If you found this project useful

Consider giving the repository a star ⭐
