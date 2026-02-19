# Mortgage Loan Trade & Profitability Analysis  
**Power BI | DAX | Power Query | Financial Analytics**

## 📌 Project Overview
This project simulates a **real-world mortgage trading and securitization workflow** used by banks and fintech lenders to determine whether loans should be sold as **whole loans to counterparties** or **bundled into UMBS securities**.

The analysis mirrors how a **trading desk and capital markets team** evaluates:
- Loan readiness
- Market benchmarking
- Trade execution decisions
- Profitability vs expectations

The project is structured as a **multi-phase case study**, progressing from data preparation to executive-level trade recommendations and profit analysis.

---

## 📂 Datasets Used
All datasets represent common internal and market data sources used by mortgage lenders and trading desks.

### 1️⃣ `loan_data`
**Purpose:** Core loan reference table  

**Key Fields:**
- `loan_id` – Unique loan identifier  
- `loan_amount` – Original loan balance  
- `property_value` – Appraised property value  
- `income_thousands` – Borrower annual income (in thousands)  
- `interest_rate` – Annual interest rate  
- `loan_term` – Loan term in months  
- `umbs_code` – Identifier used to map loans to UMBS market prices  

**Usage:**
- Loan-to-Value and Debt-to-Income calculations
- Primary dimension table for trade analysis
- Anchor for UMBS price benchmarking

---

### 2️⃣ `loan_status`
**Purpose:** Operational workflow tracking  

**Key Fields:**
- `file_in_audit`
- `file_audit_complete`
- `file_sent_to_custodian`
- `file_at_custodian`

**Usage:**
- Created a derived **Trade Status** column using nested business logic
- Identifies loans that are **ready to trade vs still in process**

---

### 3️⃣ `loan_balances`
**Purpose:** Payment schedule and amortization tracking  

**Key Fields:**
- `current_balance`
- `payment_periods_made`
- `first_payment_date`
- `next_payment_date`

**Derived Columns:**
- Payment Period
- Amortization Amount (using `PPMT`)
- Scheduled Principal Balance

**Usage:**
- Determines the **true executable balance** for trading
- Supports accurate trade and profit calculations

---

### 4️⃣ `loan_bids`
**Purpose:** Counterparty pricing for whole-loan sales  

**Key Fields (before transformation):**
- `golden_sachs`
- `storgan_manley`
- `smells_largo`
- `bank_of_americans`
- `pj_logan`

**Transformations Applied:**
- Unpivoted counterparty columns
- Normalized into:
  - `loan_id`
  - `Counterparty`
  - `Price`
- Grouped bids to identify **highest executable bid per loan**

**Usage:**
- Benchmarking whole-loan execution prices
- Trade decision comparison vs UMBS prices

---

### 5️⃣ `umbs_prices`
**Purpose:** Public market benchmark pricing  

**Key Fields:**
- `umbs_code`
- `umbs_price`

**Usage:**
- Serves as the **securitization benchmark**
- Determines whether selling to counterparties is economically superior

---

## 🔄 Data Transformation (Power Query)
- Reshaped counterparty bid data into a normalized format
- Grouped bids by loan to extract best price
- Merged UMBS benchmark pricing into the loan-level model
- Cleaned and standardized column types for modeling

All transformations were completed in **Power Query (M)** to ensure transparency and reproducibility.

---

## 🧮 Key Calculations (DAX)

### Loan Risk & Readiness Metrics
- Loan-to-Value Ratio
- Debt-to-Income Ratio
- Monthly Income normalization

### Trade Readiness Logic
- Created a **Trade Status** classification using nested `IF()` logic
- Accurately reflects post-closing operational states

### Amortization & Scheduled Balances
- Converted annual interest rates to monthly
- Used `PPMT()` to calculate principal payments
- Applied conditional logic to avoid over-amortization
- Derived Scheduled Principal Balance for trade execution

---

## 📊 Reporting & Visualization
### Loan Balances Page
- Loan ID
- Current Balance
- Scheduled Principal Balance
- Payment Dates
- Trade Status

### Trade Analysis Page
- Counterparty bid vs UMBS benchmark
- Identification of trade vs hold decisions

All visuals are formatted for **executive-level consumption** with minimal noise.

---

## 💰 Trade & Profit Analysis
The next phase of the project extends the analysis to:

- Trade Amount calculation  
- Trade Premium vs benchmark  
- Gross Loan Profit measurement  
- Target Profit benchmarking  
- Profit driver analysis using **Power BI Key Influencers**

---

## 🎯 Business Value
This project demonstrates how analytics directly supports:
- Capital markets execution
- Risk-adjusted pricing decisions
- Profitability optimization
- Leadership-level reporting

---

## 🛠 Tools & Skills Demonstrated
- Power BI (Data Modeling, DAX, AI visuals)
- Power Query (Advanced data shaping)
- Financial modeling & amortization logic
- Trade benchmarking & profitability analysis
- Executive storytelling with data
