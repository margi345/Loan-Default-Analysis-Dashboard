# Loan Default Analysis Dashboard 📊

An interactive Power BI dashboard that analyzes borrower and loan data to uncover patterns in **loan defaults, applicant demographics, and financial risk**. The project transforms raw loan application data into a 3-page executive dashboard that helps identify which borrower segments carry the highest default risk.

---

## 📌 Project Overview

Loan defaults are a major concern for financial institutions, directly affecting profitability and risk exposure. This project analyzes a loan applicant dataset to answer key business questions such as:

- Which borrower segments (age, income, employment type, education) are most likely to default?
- How does credit score relate to loan amount and default risk?
- How have loan volumes and default rates trended year over year?
- What role do factors like mortgage status, dependents, and marital status play in loan amounts and risk?

The result is a **Power BI (.pbix)** dashboard built for lenders, credit analysts, and risk management teams to explore borrower risk profiles at a glance.

---

## 🗂️ Repository Contents

| File | Description |
|---|---|
| `Loan_dataflow_project.pbix` | Power BI dashboard file containing the data model, DAX measures, and all report visuals |
| `README.md` | Project documentation (this file) — includes the full data dictionary below |

> **Note:** The raw dataset (`Loan_default.csv`) and the original Excel data dictionary are **not included** in this repo to keep it lightweight. The full column definitions and dataset statistics are documented directly in the [Dataset](#-dataset) section below instead.

---

## 📄 Dataset

**Loan Default Dataset** — contains information about borrowers who applied for loans, along with their financial status, loan characteristics, and repayment behavior.

### At a Glance

| Metric | Value |
|---|---|
| Total records | 255,347 loans |
| Time span | 2013 – 2018 (6 years, ~42,000–43,000 loans/year — evenly distributed) |
| Missing values | None — the dataset is fully complete across all 19 columns |
| Overall default rate | **11.61%** (29,653 defaults out of 255,347 loans) |
| Total loan volume | **$32.58 billion** disbursed |
| Average loan amount | **$127,579** |
| Average interest rate | ~13.5% |
| Education levels | High School, Bachelor's, Master's, PhD (near-equal split, ~63.5K–64.4K each) |
| Employment types | Full-time, Part-time, Self-employed, Unemployed |

### Column Definitions

| Column Name | Definition |
|---|---|
| `LoanID` | A unique identifier for each loan in the dataset |
| `Age` | The borrower's age at the time the loan was issued |
| `Income` | The borrower's annual income |
| `LoanAmount` | The total amount of the loan requested or approved |
| `CreditScore` | Borrower's creditworthiness score (typically 300–850); higher = more likely to repay |
| `MonthsEmployed` | Number of months the borrower has been employed at their current job |
| `NumCreditLines` | Total number of active credit lines (credit cards, loans, etc.) the borrower holds |
| `InterestRate` | The annual percentage rate (APR) charged on the loan |
| `LoanTerm` | Loan repayment period, in months |
| `DTIRatio` | Debt-to-Income ratio — debt payments relative to income; higher = more financial stress |
| `Education` | Borrower's highest level of education (High School, Bachelor's, Master's, etc.) |
| `EmploymentType` | Borrower's employment type (Full-Time, Part-Time, Self-Employed, etc.) |
| `MaritalStatus` | Borrower's marital status (Single, Married, Divorced, etc.) |
| `HasMortgage` | Whether the borrower has an existing mortgage (Yes/No) |
| `HasDependents` | Whether the borrower has dependents to support (Yes/No) |
| `LoanPurpose` | Primary reason for the loan (Home Purchase, Debt Consolidation, Education, etc.) |
| `HasCoSigner` | Whether the borrower has a co-signer on the loan (Yes/No) |
| `Default` | Whether the borrower defaulted on the loan (Yes/No) — the target/outcome variable |
| `Loan Date (DD/MM/YYYY)` | The date the loan was issued |

---

## 📊 Dashboard Structure

The `.pbix` file contains **3 report pages**, each focused on a different analytical angle:

### 1️⃣ Loan Default & Overview
A high-level summary of loan performance and default trends.
- Loan Amount by Purpose
- Average Loan Amount by Age Group
- Average Income by Employment Type
- Default Rate by Employment Type
- Default Rate by Year

### 2️⃣ Applicant Demographics & Financial Profile
A deeper look at who the borrowers are and how their profile relates to loan size and risk.
- Loans by Education Type
- Total Loan Amount by Credit Score Bin
- Total Loan Amount for Middle-Age Adults (by Mortgage / Dependents status)
- Median Loan Amount by Credit Score Bin
- Average Loan Amount for High-Credit Borrowers (by Age Group & Marital Status)

### 3️⃣ Financial Risk Metrics
Trend and risk-focused metrics for deeper financial analysis.
- YoY (Year-over-Year) Loan Amount Change
- YoY Default Loans Change
- YTD Loan Amount (by Credit Score Bin & Marital Status)
- Decomposition Tree — breaks down total Loan Amount by Income Bracket, Employment Type, and other drivers

---

## 🧮 Key Calculated Fields & Measures

Beyond the raw dataset columns, the Power BI data model includes several custom calculated columns and DAX measures to enable the analysis above:

**Calculated columns (for grouping/binning):**
- `Age Groups` — buckets borrowers into age ranges
- `Credit Score Bins` — buckets borrowers into credit score ranges
- `Income Bracket` — buckets borrowers into income ranges
- `Year` — extracted from the loan date for time-based analysis

**Key DAX measures:**
- Average Loan by Age Group
- Average Income by Employment Type
- Default Rate by Employment Type
- Default Rate by Year
- Loans by Education Type
- Total Loan (Credit Bins)
- Median by Credit Score Bins
- Average Loan Amount (High Credit)
- YoY Loan Amount Change
- YoY Default Loans Change
- YTD Loan Amount

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — data modeling, DAX measures, and report visualization
- **Excel** — source data dictionary / column definitions
- **DAX (Data Analysis Expressions)** — for calculated columns and measures
- **Power Query** — data shaping/transformation within the Power BI dataflow

---

## 💡 Key Findings

Based on analysis of all 255,347 loan records (overall default rate: **11.61%**):

**Age is the strongest single risk signal.**
Default rate drops sharply and consistently as age increases:

| Age Group | Default Rate |
|---|---|
| 18–25 | **20.76%** |
| 26–35 | 16.08% |
| 36–45 | 11.55% |
| 46–55 | 8.45% |
| 56–65 | 5.86% |
| 66+ | 4.60% |

Borrowers aged 18–25 default at over **4.5x the rate** of borrowers 66+.

**Employment status matters more than income level.**
Unemployed borrowers default at **13.55%** vs. **9.46%** for full-time employees — despite average income being nearly identical across all employment types (~$82K–$83K). This suggests employment *stability*, not income *amount*, is the bigger driver of risk.

**Credit score is directionally predictive, but the effect is modest.**
Default rate declines from **12.47%** (Poor: 300–579) to **9.81%** (Exceptional: 800–850) — a real but smaller gap than expected, meaning credit score alone isn't a strong standalone predictor in this dataset.

**Support structures reduce default risk:**
- Borrowers **with a co-signer**: 10.36% default vs. **12.87%** without
- Borrowers **with dependents**: 10.50% default vs. **12.72%** without
- Borrowers **with a mortgage**: 10.88% default vs. **12.35%** without

**Education level shows a mild inverse relationship with default:**
High School (12.88%) → Bachelor's (12.10%) → Master's (10.87%) → PhD (10.59%).

**Marital status:** Married borrowers default least often (10.40%), followed by Single (11.91%) and Divorced (12.53%).

**Loan purpose:** Business loans have the highest default rate (12.33%); Home loans have the lowest (10.23%).

**Defaulted loans, on average, carry:**
- Lower credit scores (559 vs. 576 for non-defaults)
- Higher interest rates (15.90% vs. 13.18%)
- Slightly higher DTI ratio (0.512 vs. 0.499)

**Loan volume and default rate are both stable year over year** (2013–2018) — default rate holds steady in the 11.5%–11.75% range with no major trend, while total annual loan volume fluctuates by only ±1–2% year to year (ranging from $5.37B to $5.48B annually).

**Loan amount itself is not segment-driven** — average loan size stays remarkably flat (~$126K–$128K) across every age group, loan purpose, and credit tier, suggesting loan amount was likely generated independently of borrower risk profile in this dataset rather than being sized to it.

---

## 👤 Author

**Your Name**
🔗 https://github.com/margi345  

---

## 📜 License

This project is licensed under the [MIT License](LICENSE) — feel free to use, modify, and share with attribution.
