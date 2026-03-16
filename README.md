# 🏦 Banking Risk Analytics Dashboard

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**A comprehensive Power BI risk analytics dashboard for banking that evaluates loan repayment likelihood using interconnected client, banking, gender, advisor, and period data — paired with Python-based Exploratory Data Analysis.**

[📊 View Dashboard](#-dashboard-structure) · [🚀 Get Started](#-getting-started) · [📁 Project Structure](#-project-structure) · [📬 Contact](#-contact--support)

</div>

---

## 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Key Features](#-key-features)
3. [Key Performance Indicators (KPIs)](#-key-performance-indicators-kpis)
4. [Data Transformation & Feature Engineering](#-data-transformation--feature-engineering)
5. [Dashboard Structure](#-dashboard-structure)
6. [Technical Architecture](#-technical-architecture)
7. [Getting Started](#-getting-started)
8. [Project Structure](#-project-structure)
9. [Business Applications](#-business-applications)
10. [Key Insights Provided](#-key-insights-provided)
11. [Dataset Overview](#-dataset-overview)
12. [Technologies Used](#-technologies-used)
13. [Installation & Usage](#-installation--usage)
14. [Future Enhancements](#-future-enhancements)
15. [Contributing](#-contributing)
16. [License](#-license)
17. [Contact & Support](#-contact--support)
18. [Acknowledgments](#-acknowledgments)

---

## 🔍 Project Overview

The **Banking Risk Analytics Dashboard** is an end-to-end business intelligence solution that empowers financial institutions to make data-driven lending decisions. By integrating interconnected datasets — clients, banking relationships, gender demographics, investment advisors, and time periods — the dashboard delivers a 360° view of portfolio risk and client health.

### 💡 Business Value

| Challenge | Solution |
|-----------|----------|
| High default risk in loan portfolios | Income Band & Risk Weighting analytics |
| Opaque client relationship health | Engagement Timeframe metric |
| Manual, error-prone fee calculations | Automated Processing Fees calculation |
| Fragmented view of deposits & loans | Unified multi-dashboard reporting |
| Slow credit approval decisions | At-a-glance KPI summary dashboards |

The project combines a **Power BI interactive dashboard** (in the `Banking/` directory) with **Python Jupyter Notebooks** for in-depth Exploratory Data Analysis, offering both executive-level summaries and analyst-level deep dives.

---

## ✨ Key Features

- 📊 **4 Interconnected Power BI Dashboards** — Home, Loan Analysis, Deposit Analysis, and Summary
- 🔗 **Star-Schema Data Model** — 5 linked tables (clients, banking relationships, gender, advisors, periods) with optimized foreign key relationships
- 🧮 **Advanced DAX Calculations** — Engagement Timeframe, Income Band, Processing Fees, and aggregate loan/deposit measures
- 🎛️ **Dynamic Filtering & Slicers** — Real-time drill-down by time period, client demographics, product type, and risk tier
- 🎨 **Conditional Formatting** — Color-coded risk indicators for at-a-glance decision-making
- 🐍 **Python EDA Notebooks** — Two iterative versions of exploratory analysis on 3,000+ banking client records
- 📂 **Comprehensive Raw Datasets** — Normalized CSV files for clients, relationships, gender, and advisors
- 📄 **Presentation-Ready Exports** — PDF dashboard, PowerPoint, Word report, and Excel data files

---

## 📈 Key Performance Indicators (KPIs)

### 👥 Client Metrics

| KPI | Description |
|-----|-------------|
| **Total Clients** | Distinct count of all active banking clients |
| **Engagement Days** | Relationship duration in days (date joined → today) |
| **Income Band** | Categorized income tier (Low / Mid / High) |
| **Loyalty Classification** | Client tier (Jade, Silver, Gold, Platinum) |
| **Risk Weighting** | Client-level credit risk score |

### 💳 Loan Portfolio KPIs

| KPI | Description |
|-----|-------------|
| **Total Loan Amount** | Combined bank loans + business lending + credit card balances |
| **Bank Loan** | Traditional lending portfolio value |
| **Business Lending** | SME and commercial lending portfolio |
| **Credit Card Balance** | Revolving credit exposure |
| **Loan-to-Income Ratio** | Risk ratio by client segment |
| **Processing Fees** | Fee income generated per client (5% for High fee structure) |

### 🏦 Deposit Analysis KPIs

| KPI | Description |
|-----|-------------|
| **Total Deposits** | Aggregated deposits across all account types |
| **Bank Deposits** | Primary bank account balances |
| **Savings Account Balance** | Savings product balances |
| **Checking Account Balance** | Transactional account balances |
| **Foreign Currency Account** | Multi-currency deposit exposure |
| **Deposit-to-Loan Ratio** | Liquidity and stability indicator |

### 💰 Revenue Metrics

| KPI | Description |
|-----|-------------|
| **Total Processing Fees** | Total fee revenue across the portfolio |
| **Fee Structure Performance** | Revenue by High vs. standard fee clients |
| **Revenue per Segment** | Profitability by Income Band and Loyalty tier |
| **Superannuation Savings** | Client retirement savings tracked |

---

## ⚙️ Data Transformation & Feature Engineering

### 🕐 Engagement Timeframe Metric

Measures how long a client has been with the bank, categorized into engagement tiers for segmentation and retention analysis.

```dax
Engagement Days = DATEDIFF([Joined Bank], TODAY(), DAY)
```

Clients are bucketed into:
- 🟢 **New** — < 1 year
- 🟡 **Developing** — 1–5 years
- 🔵 **Established** — 5–10 years
- 🟣 **Long-Term** — > 10 years

---

### 💵 Income Band Categorization

A critical variable for risk assessment and client segmentation:

```dax
Income Band =
    IF([Estimated Income] < 100000, "Low Income",
    IF([Estimated Income] <= 300000, "Mid Income",
    "High Income"))
```

| Band | Income Range | Risk Profile |
|------|-------------|--------------|
| 🔴 Low Income | < $100,000 | Higher default risk |
| 🟡 Mid Income | $100,000 – $300,000 | Moderate risk |
| 🟢 High Income | > $300,000 | Lower default risk |

---

### 🧾 Processing Fees Calculation

Dynamic fee calculation tied to client fee structure and total loan exposure:

```dax
Processing Fees =
    IF([Fee Structure] = "High",
       [Total Loans] * 0.05,
       [Total Loans] * 0.02)
```

---

### 📊 Total Loan & Deposit Aggregation

```dax
Total Loans = [Bank Loans] + [Business Lending] + [Credit Card Balance]

Total Deposits = [Bank Deposits] + [Saving Accounts]
              + [Checking Accounts] + [Foreign Currency Account]
```

---

## 🖥️ Dashboard Structure

The solution is organized into **4 interconnected dashboards**, each designed for a distinct audience and use case.

---

### 1️⃣ Home Dashboard

> *Executive summary for at-a-glance decision-making*

- 📌 Total client count and distribution overview
- 📌 Key risk indicators and portfolio health snapshot
- 📌 Quick-access navigation to detailed dashboards
- 📌 Headline KPIs: Total Loans, Total Deposits, Processing Fees
- 📌 Client breakdown by Income Band and Loyalty Classification

---

### 2️⃣ Loan Analysis Dashboard

> *Deep-dive into lending portfolio and risk exposure*

- 💳 Portfolio breakdown — Bank Loans vs. Business Lending vs. Credit Cards
- 📊 Risk assessment — Income Band vs. Loan Amounts (scatter/bar charts)
- 💰 Fee income analysis by fee structure and client tier
- 👥 Client segmentation by loan distribution and Risk Weighting
- 📈 Loan-to-income ratio trends across advisor segments

---

### 3️⃣ Deposit Analysis Dashboard

> *Insights into client deposit patterns and liquidity*

- 🏦 Deposit composition — Savings vs. Checking vs. Foreign Currency vs. Bank Deposits
- 📅 Client engagement analysis — relationship duration vs. deposit amounts
- 🗂️ Account type distribution across demographics and advisors
- 📉 Deposit-to-Loan ratio for liquidity health monitoring
- 🔄 Cross-product usage patterns for upsell/retention insights

---

### 4️⃣ Summary Dashboard

> *Consolidated strategic overview for senior management*

- 🎯 Consolidated KPI scorecard across all banking operations
- ⚠️ Risk concentration alerts and portfolio health indicators
- 📋 Advisor performance comparison
- 🌍 Client nationality and demographic distribution
- 🏆 Loyalty tier performance and segment profitability

---

## 🏗️ Technical Architecture

### Data Model — Star Schema

```
                    ┌─────────────┐
                    │   Period    │
                    │  (temporal) │
                    └──────┬──────┘
                           │
┌──────────────┐    ┌──────▼──────┐    ┌────────────────┐
│    Gender    │────│   Clients   │────│   Investment   │
│ (dimension)  │    │   (fact)    │    │    Advisors    │
└──────────────┘    └──────┬──────┘    └────────────────┘
                           │
                    ┌──────▼──────┐
                    │   Banking   │
                    │Relationship │
                    └─────────────┘
```

### Table Relationships

| From Table | Key | To Table | Relationship |
|------------|-----|----------|--------------|
| `Clients` | `GenderId` | `Gender` | Many-to-One |
| `Clients` | `IAId` | `Investment Advisors` | Many-to-One |
| `Clients` | `BRId` | `Banking Relationship` | Many-to-One |
| `Clients` | `Joined Bank` | `Period` | Many-to-One |

### Power BI Features Used

| Feature | Application |
|---------|-------------|
| **DAX Measures** | KPI calculations, Income Band, Engagement Days |
| **Calculated Columns** | Fee structure flags, loan aggregations |
| **Slicers** | Time period, demographics, product type, advisor |
| **Conditional Formatting** | Color-coded risk tiers |
| **Drill-through Pages** | Client-level detail from summary views |
| **Bookmarks** | Navigation between dashboard pages |
| **Tooltips** | Enhanced hover-over data context |
| **Relationships** | Cross-filter propagation across tables |

---

## 🚀 Getting Started

### Prerequisites

| Tool | Version | Purpose |
|------|---------|---------|
| [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/) | Latest | Dashboard viewing & editing |
| [Python](https://python.org) | 3.8+ | Running EDA notebooks |
| [Jupyter Notebook](https://jupyter.org) | Latest | Notebook environment |
| [pandas](https://pandas.pydata.org) | 1.3+ | Data manipulation |
| [matplotlib](https://matplotlib.org) / [seaborn](https://seaborn.pydata.org) | Latest | Visualizations |

### Implementation Steps

**For the Power BI Dashboard:**

1. **Clone the repository**
   ```bash
   git clone https://github.com/Yash-Padme/Banking-Analysis.git
   cd Banking-Analysis
   ```

2. **Open Power BI Desktop**

3. **Load the project file**
   ```
   File → Open → Banking/Banking Dashboard (2025).pbix
   ```

4. **Refresh the data** (if prompted) by pointing to the CSV files in `Banking/raw datasets/`

5. **Explore the dashboards** using the navigation buttons on the Home page

---

**For the Python EDA Notebooks:**

1. **Install dependencies**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

2. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

3. **Open the notebooks**
   - `BankEDA_Version_1.ipynb` — Initial exploratory analysis
   - `BankEDA_Version_2.ipynb` — Enhanced analysis with advanced visualizations

---

## 📁 Project Structure

```
Banking-Analysis/
│
├── 📓 BankEDA_Version_1.ipynb        # Initial Python EDA notebook (~1.2 MB)
├── 📓 BankEDA_Version_2.ipynb        # Enhanced Python EDA notebook (~2.2 MB)
├── 📊 Banking.csv                    # Primary banking dataset (~577 KB)
├── 📄 DashBoard.pdf                  # Dashboard export in PDF format
├── 📋 .gitignore                     # Git ignore configuration
│
└── 📂 Banking/                       # Power BI project directory
    ├── 📊 Banking Dashboard (2025).pbix   # Power BI project file (~975 KB)
    ├── 📝 Banking Report.docx             # Detailed written report
    ├── 📊 Banking.csv                     # Dataset copy for Power BI
    ├── 📈 Banking.xlsx                    # Excel-formatted dataset (~704 KB)
    ├── 📑 Banking.pptx                    # PowerPoint presentation
    ├── 👥 clients.csv                     # Client lookup table
    │
    └── 📂 raw datasets/                   # Normalized source data
        ├── 🗄️ banking-clients.csv         # Full client records (~577 KB)
        ├── 🔗 banking-realtionships.csv   # Banking relationship types
        ├── 🚻 gender.csv                  # Gender dimension table
        └── 👔 investment-advisiors.csv    # Advisor dimension table
```

---

## 💼 Business Applications

### 🛡️ Risk Management

| Use Case | How the Dashboard Helps |
|----------|------------------------|
| **Credit Approval** | Assess repayment likelihood using Income Band, Risk Weighting, and loan-to-income ratios |
| **Portfolio Monitoring** | Track loan performance across Income Bands and Banking Relationship types |
| **Risk Mitigation** | Identify high-risk clients and portfolio concentration areas |
| **Default Prevention** | Early warning signals from deposit-to-loan ratio trends |

### 🤝 Customer Relationship Management (CRM)

| Use Case | How the Dashboard Helps |
|----------|------------------------|
| **Client Segmentation** | Categorize by Loyalty Classification (Jade / Silver / Gold / Platinum) |
| **Engagement Tracking** | Monitor relationship duration and product cross-usage |
| **Retention Strategy** | Focus resources on long-tenure, high-deposit clients |
| **Product Optimization** | Tailor offerings based on account type preferences |

### ⚡ Operational Efficiency

| Use Case | How the Dashboard Helps |
|----------|------------------------|
| **Revenue Optimization** | Maximize processing fee income from high-fee structure clients |
| **Advisor Performance** | Compare portfolio metrics across Investment Advisors |
| **Resource Allocation** | Direct efforts toward the most profitable client segments |
| **Regulatory Reporting** | Structured data model supports compliance and audit needs |

---

## 💡 Key Insights Provided

### 📊 Client Behavior Analysis
- Income distribution across the entire client base segmented by demographics
- Average engagement duration and product adoption patterns by tenure tier
- Cross-product usage rates (savings + checking + foreign currency + loans)
- Loyalty tier transitions and retention risk indicators

### ⚠️ Risk Assessment
- Loan-to-income ratios by client segment and banking relationship type
- Processing fee impact on client profitability and net margin
- Deposit stability as an indicator of credit risk
- Client concentration risk by advisor and banking relationship

### 🧭 Strategic Intelligence
- Advisor portfolio comparison for performance management
- Nationality and demographic distribution for market expansion insights
- Product performance and cross-selling opportunity identification
- Fee structure revenue contribution vs. standard-fee clients

---

## 🗃️ Dataset Overview

The project uses a normalized banking dataset with **3,000+ client records** across interconnected tables:

### Primary Dataset: `banking-clients.csv`

| Column | Type | Description |
|--------|------|-------------|
| `Client ID` | String | Unique client identifier |
| `Name` | String | Client full name |
| `Age` | Integer | Client age |
| `Location ID` | Integer | Geographic location reference |
| `Joined Bank` | Date | Date client joined the bank |
| `Banking Contact` | String | Assigned banking contact |
| `Nationality` | String | Client nationality |
| `Occupation` | String | Client profession |
| `Fee Structure` | String | `High` or standard fee tier |
| `Loyalty Classification` | String | Jade / Silver / Gold / Platinum |
| `Estimated Income` | Float | Annual income estimate |
| `Superannuation Savings` | Float | Retirement savings balance |
| `Credit Card Balance` | Float | Revolving credit balance |
| `Bank Loans` | Float | Traditional loan balance |
| `Bank Deposits` | Float | Primary bank deposit balance |
| `Checking Accounts` | Float | Checking account balance |
| `Saving Accounts` | Float | Savings account balance |
| `Foreign Currency Account` | Float | Foreign currency deposit |
| `Business Lending` | Float | SME lending balance |
| `Properties Owned` | Integer | Number of properties |
| `Risk Weighting` | Integer | Credit risk score (1–5) |
| `BRId` | Integer | Banking Relationship FK |
| `GenderId` | Integer | Gender dimension FK |
| `IAId` | Integer | Investment Advisor FK |

### Dimension Tables

| Table | Columns | Values |
|-------|---------|--------|
| `gender.csv` | GenderId, Gender | Male, Female |
| `banking-realtionships.csv` | BRId, Banking Relationship | Retail, Institutional, Private Bank, Commercial |
| `investment-advisiors.csv` | IAId, Investment Advisor | 10+ named advisors |

---

## 🛠️ Technologies Used

| Category | Technology | Purpose |
|----------|-----------|---------|
| **BI & Visualization** | Microsoft Power BI Desktop | Interactive dashboards |
| **Query Language** | DAX (Data Analysis Expressions) | Calculated measures & columns |
| **Data Language** | Power Query (M) | Data transformation & loading |
| **Programming** | Python 3.x | Exploratory data analysis |
| **Notebook** | Jupyter Notebook | Interactive Python analysis |
| **Data Manipulation** | pandas | DataFrame operations |
| **Numerical Computing** | NumPy | Statistical calculations |
| **Visualization** | Matplotlib, Seaborn | Charts and plots |
| **Data Format** | CSV, XLSX | Source data storage |
| **Documentation** | PDF, DOCX, PPTX | Reporting and presentation |
| **Version Control** | Git / GitHub | Source control |

---

## ⚙️ Installation & Usage

### Power BI Dashboard

```bash
# 1. Clone the repository
git clone https://github.com/Yash-Padme/Banking-Analysis.git

# 2. Navigate to the project directory
cd Banking-Analysis

# 3. Open Power BI Desktop and load the .pbix file
#    File → Open Report → Banking/Banking Dashboard (2025).pbix

# 4. If data refresh is needed, update the data source path to:
#    Banking/raw datasets/banking-clients.csv
```

### Python EDA Notebooks

```bash
# 1. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

# 2. Install required packages
pip install pandas numpy matplotlib seaborn jupyter openpyxl

# 3. Launch Jupyter Notebook
jupyter notebook

# 4. Open and run the notebooks:
#    - BankEDA_Version_1.ipynb  (initial analysis)
#    - BankEDA_Version_2.ipynb  (enhanced analysis)
```

### Quick Data Exploration

```python
import pandas as pd

# Load the banking dataset
df = pd.read_csv('Banking/raw datasets/banking-clients.csv')

# Quick overview
print(df.shape)           # (rows, columns)
print(df.describe())      # Summary statistics
print(df.dtypes)          # Column data types

# Income Band distribution
bins = [0, 100000, 300000, float('inf')]
labels = ['Low Income', 'Mid Income', 'High Income']
df['Income Band'] = pd.cut(df['Estimated Income'], bins=bins, labels=labels)
print(df['Income Band'].value_counts())
```

---

## 🔮 Future Enhancements

### Phase 1 — Advanced Analytics
- [ ] 🤖 Machine learning model integration for loan default prediction
- [ ] 📊 Real-time risk scoring for new credit applications
- [ ] 🔮 Predictive modeling for client churn probability
- [ ] 📉 Time-series forecasting for deposit and loan trends

### Phase 2 — Expanded Scope
- [ ] 🗺️ Geographic heat-map analysis of client distribution
- [ ] 🏦 Competitor benchmarking integration
- [ ] 📋 Regulatory compliance and stress-test reporting modules
- [ ] 🌐 Multi-branch / multi-region segmentation

### Phase 3 — Technical Improvements
- [ ] ⚡ Automated data refresh pipelines (Power BI Gateway / Dataflows)
- [ ] 📱 Mobile-responsive dashboard design (Power BI Mobile)
- [ ] 🎨 Advanced custom visuals (Deneb, Charticulator)
- [ ] 🔄 Real-time data streaming via Power BI Streaming Datasets
- [ ] ☁️ Azure Synapse or Fabric integration for enterprise scale

---

## 🤝 Contributing

Contributions are warmly welcome! Here's how to get involved:

1. **Fork** the repository
   ```bash
   git fork https://github.com/Yash-Padme/Banking-Analysis.git
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes** — ensure they follow the existing code style and data model conventions

4. **Test your changes** — validate DAX measures and Python outputs

5. **Commit with a clear message**
   ```bash
   git commit -m "feat: add geographic analysis to Summary dashboard"
   ```

6. **Push and open a Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```

### Contribution Guidelines

- 📐 Follow the existing Power BI naming conventions for measures and calculated columns
- 🐍 Use PEP 8 style for all Python code contributions
- 📝 Document new DAX measures with inline comments
- ✅ Include sample output or screenshots for dashboard changes
- 🔒 Do not commit sensitive or real client data

---

## 📜 License

This project is licensed under the **MIT License** — see below for details.

```
MIT License

Copyright (c) 2026 Yash-Padme

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

---

## 📬 Contact & Support

<div align="center">

| Channel | Details |
|---------|---------|
| 👤 **Author** | Yash Padme |
| 🐙 **GitHub** | [@Yash-Padme](https://github.com/Yash-Padme) |
| 📁 **Repository** | [Banking-Analysis](https://github.com/Yash-Padme/Banking-Analysis) |

</div>

### 🐛 Reporting Issues

Found a bug or have a feature request?
1. Check the [existing issues](https://github.com/Yash-Padme/Banking-Analysis/issues) first
2. Open a [new issue](https://github.com/Yash-Padme/Banking-Analysis/issues/new) with:
   - A clear, descriptive title
   - Steps to reproduce (for bugs)
   - Expected vs. actual behavior
   - Power BI version or Python version (as applicable)

---

## 🙏 Acknowledgments

- 🏦 **Banking Domain Inspiration** — [JamesMatini/Banking-Analysis-Dashboard-by-PowerBI-](https://github.com/JamesMatini/Banking-Analysis-Dashboard-by-PowerBI-) for the Power BI dashboard design patterns and feature engineering concepts
- 📊 **Microsoft Power BI Community** — For DAX best practices, optimization tips, and custom visual resources
- 🐍 **Python Data Science Community** — pandas, matplotlib, seaborn, and Jupyter for enabling rapid EDA iteration
- 📚 **Open Banking Datasets** — For providing realistic financial data structures used in analysis
- 🎓 **Risk Management Literature** — Basel III / IV frameworks for credit risk weighting concepts

---

<div align="center">

**⭐ If you found this project helpful, please consider giving it a star!**

Made with ❤️ for the data analytics and banking community

![Footer](https://img.shields.io/badge/Banking%20Risk%20Analytics-Power%20BI%20%7C%20Python-blue?style=flat-square)

</div>
