# Employee Salary Analysis Dashboard (Power BI)

An interactive Power BI report that shows how much a multi-business-unit company spends on salary, and where that money goes: base pay, allowances, overtime, deductions and staff loans.

> **Note on the data:** This project uses a **fully synthetic payroll dataset**. It mirrors the structure of a real HR/payroll extract, but no real employee, company or salary figure appears in it. The goal is to demonstrate the analysis approach, so the findings below describe this dataset, not any real organisation.

---

## Business Problem

Payroll is usually one of the biggest costs a business has, but the raw numbers sit in one wide table that is hard to read. Leadership wants to answer:

- How much are we spending on salary, and how is that split across business units, departments and grades?
- How much of gross pay is take-home, and how much goes to tax, pension and loan repayments?
- How much do we rely on overtime and allowances?
- Are staff loans a meaningful share of deductions?

This report answers those questions in six pages.

## Dataset

| Detail | Value |
|---|---|
| Source file | `Synthetic_Employee_Salary_Dataset.xlsx` (sheet: `Salary Data`) |
| Grain | One row per employee per month |
| Rows | 4,932 (822 employees x 6 months) |
| Period | October 2025 to March 2026 |
| Columns | 24 |

**Field groups**

- **Employee and org structure:** `EMP_NO`, `EMP_GRADE_NAME`, `BUSINESS_UNIT`, `FUNCTION_DEPT`, `EMP_CATEGORY` (Plant / Non Plant), `MONTH_YEAR`
- **Earnings:** `TOTAL_OT`, `COLA`, `SHF_ALL` (shift allowance), `DISTURB_ALL`, `HAZARDOUS`, `OTHER_EARN`, `TOTAL_EARNINGS`
- **Deductions:** `INCOME_TAX`, `PENSION`, `COOP_DEDN`, `UNION_DUES`, `VEHICLE_LOAN`, `RENT_LOAN`, `COMPASSIONATE_LOAN`, `OTHER_DEDN`, `TOTAL_DEDUCTIONS`
- **Derived totals:** `TOTAL_LOAN`, `NET_SALARY`

`NET_SALARY = TOTAL_EARNINGS - TOTAL_DEDUCTIONS`. The data has no missing values, and the totals reconcile exactly.

## Data Model

- A central **fact table** holds the monthly payroll records.
- **Dimension tables** (for example business unit, department, grade, employee and month) are linked to the fact table in a star schema, so every visual can be filtered the same way.
- Separate **earnings** and **deductibles** tables break the pay components into categories, which powers the breakdown charts.
- **DAX measures** calculate the headline numbers: total and average net salary, gross earnings, total deductions, overtime, loans and headcount.

![Data Model 1](SALARY%20PROJECT/images/Data%20Model%201.png)
![Data Model 2 (Calculated Tables)](SALARY%20PROJECT/images/Data%20Model%202.png)

## Dashboard Pages

| # | Page | What it shows |
|---|---|---|
| 1 | Employee Count Summary | Headcount by grade, department and month, with a business unit slicer |
| 2 | Net Salary Analysis | Total and average net salary, monthly trend, split by business unit and department |
| 3 | Net Salary vs Gross Salary and Deductions | Gross to net bridge, earnings and deduction breakdowns, key influencers |
| 4 | Employee Overtime Analysis | Overtime by department, a decomposition tree, top overtime earners |
| 5 | Loan Analysis | Loan types by business unit, loan categories, monthly loan trend |
| 6 | Gross Earnings and Allowances / Deductibles | Allowance mix, top deductions, key influencers |

![Employee Count](SALARY%20PROJECT/images/Employee%20Count.png)
![Net Salary Analysis by Business Unit](SALARY%20PROJECT/images/Net%20Salary%20Analysis.png)
![Earnings vs Deductions](SALARY%20PROJECT/images/Earnings%20vs%20Deductions.png)
![Overtime Analysis](SALARY%20PROJECT/images/Overtime%20Analysis.png)
![Loan Analysis](SALARY%20PROJECT/images/Loan%20Analysis.png)
![Earnings & Allowances](SALARY%20PROJECT/images/Earnings%20and%20Allowances.png)
![Deductibles Breakdown](SALARY%20PROJECT/images/Deductibles.png)

## Key Insights

1. **Total spend:** Staff earned **1.51bn** gross over the six months. After **433.85M** in deductions, **1.08bn** was paid out as net salary, about **71%** of gross.
2. **Average pay:** The average net salary is about **218K per employee per month**. Monthly net payroll stays within a narrow band (roughly **177M to 181M**), so there are no dramatic swings across the period.
3. **Where the money goes:** Alpha Industries accounts for about **49%** of net pay (524.94M), Beta Manufacturing about **37%** (397.57M) and Gamma Holdings about **14%** (153.38M). Each unit's share of pay closely matches its share of headcount, so pay per head is similar across units.
4. **Departments:** Operations (258 staff) and Engineering (194 staff) are the two largest cost centres, together about **55%** of net pay. On average pay per head, Engineering (about 228K) and Commercial (about 227K) are highest, and Finance and Accounts (about 203K) is lowest.
5. **Grades:** Average net pay rises sharply with seniority, from about **105K** for Grade I/Trainee to about **368K** for Grade IV A, roughly 3.5 times higher.
6. **Overtime is the largest add-on:** Overtime totals **102.85M**, about **41%** of all allowances (the five allowance types together total about 248M) and about **7%** of gross earnings. It is concentrated in Operations (31.03M) and Engineering (25.22M).
7. **Overtime is unevenly shared:** The top 10% of employees receive about **28%** of all overtime pay. Across the period, the highest earner averages around 90K a month in overtime alone.
8. **Deductions:** Income tax (**150.97M**, about 35%) and pension (**120.78M**, about 28%) make up roughly 63% of all deductions. Both are percentage-based, so they rise with earnings.
9. **Loans:** Staff loans total **105.00M**, about **24%** of deductions. Vehicle loans are the largest type (44.30M), followed by rent (38.22M) and compassionate loans (22.49M). Vehicle loan repayments trend upward over the six months. Roughly **56%** of employee-months include a loan repayment.
10. **Key influencers:** Power BI's key influencers visual shows that overtime is the strongest driver of higher total earnings, and that loan repayments are the strongest driver of total deductions.

## Tools and Skills Demonstrated

- **Power BI Desktop:** star schema modelling, DAX measures, slicers, decomposition trees, key influencers, drill-through style navigation
- **Data modelling:** fact and dimension tables, separate earnings and deduction tables
- **Financial and HR analytics:** payroll cost analysis, gross to net reconciliation, overtime and loan analysis

## How to Use

1. Download the Power BI file (`.pbix`) from this repository and open it in Power BI Desktop.
2. If you want to rebuild it, import the `Salary Data` sheet from `Synthetic_Employee_Salary_Dataset.xlsx` and recreate the model described above.
3. Use the month and business unit slicers on each page to filter the numbers.
4. You can add the canvas back ground by importing 

A PDF export of the report is also included: `salary_project_portfolio.pdf`.

## Possible Next Steps

- Add a department-level view of overtime as a share of base pay to spot teams that rely on it most.
- Track loan repayments against net pay to show how much of take-home goes to repayments.
- Add a forecast of next quarter's payroll cost.

## Author

**Chris**
