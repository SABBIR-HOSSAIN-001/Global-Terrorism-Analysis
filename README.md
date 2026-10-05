# 🌍 Global Terrorism Analysis

An end-to-end data analytics project analyzing global terrorism incidents from **1970 to 2017** using **Python, PostgreSQL, SQL, and Power BI**.

The project covers data validation, SQL-based cleaning and feature engineering, and an interactive Power BI dashboard for exploring attack patterns across time, regions, countries, severity levels, and attack types.

---

## 📊 Dashboard Preview

![Global Terrorism Overview Dashboard](powerbi/screenshots/Screenshot_power_bi.png)

### Dashboard at a Glance

| KPI | Value |
| --- | ---: |
| Total Attacks | 171K (171,055) |
| Total Killed | 386K |
| Total Wounded | 500K |
| Avg Casualties per Attack | 5.18 |

**Visuals on the Global Overview page**

- **Global Terrorist Attacks by Country**: filled map showing attack intensity by country
- **Attack Severity Distribution**: donut chart (Low / Medium / High)
- **Global Terrorist Attacks, Yearly Trend**: line chart of attacks per year
- **Attacks by Region**: ranked bar chart of attack counts per region

**Interactive controls**

- Select Decade
- Select Year (range slider, 1970–2017)
- Select Country
- Select Attack Type
- Reset button to clear all filters

---

## 📌 Project Overview

This project analyzes the Global Terrorism Database (GTD) to answer questions such as:

- How did terrorism incidents change over time?
- Which regions and countries experienced the most attacks?
- How severe were attacks in terms of casualties?
- Which attack types were most common?
- How many attacks were successful vs. failed?

**Workflow**

```text
Raw GTD Dataset
      ↓
Python Data Inspection & Validation
      ↓
PostgreSQL Import (raw_gtd_events)
      ↓
SQL Cleaning (gtd_clean)
      ↓
Feature Engineering
      ↓
Analysis View (vw_gtd_analysis)
      ↓
Power BI Data Model + DAX
      ↓
Interactive Dashboard
```

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
| --- | --- |
| Python (Pandas) | Data loading, inspection, and validation |
| PostgreSQL | Data storage and analytical processing |
| SQL | Cleaning, transformation, and feature engineering |
| Power BI | Interactive dashboard and visualization |
| DAX | KPI and analytical measures |
| GitHub | Version control and documentation |

---

## 📂 Project Structure

```text
Global-Terrorism-Analysis/
│
├── data/
│   └── data_loading_by_python.ipynb
│
├── sql/
│   └── sql_raw.txt
│
├── powerbi/
│   ├── Global_Terrorism_Analysis_BI.pbix
│   └── screenshots/
│       └── Screenshot_power_bi.png
│
└── README.md
```

| Folder | Contents |
| --- | --- |
| `data/` | Python notebook used to load and inspect the GTD dataset |
| `sql/` | SQL script for the PostgreSQL workflow (raw table, cleaning, feature engineering, analysis view) |
| `powerbi/` | Power BI report file and dashboard screenshot |

---

## 📁 Dataset

**Global Terrorism Database (GTD)**

| Item | Detail |
| --- | --- |
| Time period | 1970–2017 |
| Original records | 171,056 |
| Columns | 135 |
| Valid records imported | 171,055 |
| Malformed records skipped | 1 |

One malformed record was found during CSV validation and excluded from the PostgreSQL import.

> **Note:** The raw GTD dataset is **not included** in this repository. Please obtain it from the official source and follow its licensing and usage terms.

---

## 🐍 Python: Data Inspection

Python was used to load the CSV, check dimensions and data types, detect duplicates and missing values, and find malformed records before importing into PostgreSQL. The notebook is in [`data/data_loading_by_python.ipynb`](data/data_loading_by_python.ipynb).

```python
import pandas as pd

gtd = pd.read_csv(
    "globalterrorismdb_0718dist.csv",
    encoding="latin1",
    low_memory=False
)

print("Rows:", gtd.shape[0])
print("Columns:", gtd.shape[1])
```

---

## 🗄️ PostgreSQL & SQL

**Database:** `gtd_db`

```text
raw_gtd_events  →  gtd_clean  →  vw_gtd_analysis
```

Raw data was first imported as text, then cleaned and typed in SQL. The SQL workflow is in [`sql/sql_raw.txt`](sql/sql_raw.txt).

**Cleaning tasks**

- Converted fields to proper numeric and date types
- Handled missing casualty values
- Converted invalid property values (`-99`) to `NULL`
- Created standardized event dates
- Validated event IDs, coordinates, and year ranges
- Checked for duplicate records

**Engineered features**

| Feature | Logic |
| --- | --- |
| `total_casualties` | `killed + wounded` |
| `attack_severity` | Low = 0 casualties, Medium = 1–10, High = more than 10 |
| `decade` | 1970s, 1980s, 1990s, 2000s, 2010s |
| `attack_outcome` | Based on success and suicide-attack indicators |

---

## 🔍 Data Validation Results

| Check | Result |
| --- | --- |
| Total valid rows | 171,055 |
| Duplicate event IDs | 0 |
| Duplicate rows | 0 |
| Minimum year | 1970 |
| Maximum year | 2017 |
| Missing latitude | 0 |
| Missing longitude | 0 |

---

## 📈 Key Findings

### Attacks by Decade

| Decade | Attacks |
| --- | ---: |
| 1970s | 9,914 |
| 1980s | 31,160 |
| 1990s | 28,762 |
| 2000s | 25,040 |
| 2010s | 76,179 |

### Attack Severity

| Severity | Attacks | Share |
| --- | ---: | ---: |
| Medium | 83,162 | 48.62% |
| Low | 69,961 | 40.90% |
| High | 17,932 | 10.48% |

### Attack Outcome

| Outcome | Attacks |
| --- | ---: |
| Successful Attack | 148,211 |
| Failed Attack | 17,021 |
| Successful Suicide Attack | 4,991 |
| Failed Suicide Attack | 832 |

### Top Regions by Attack Count

| Region | Attacks |
| --- | ---: |
| Middle East & North Africa | ~47K |
| South Asia | ~42K |
| South America | ~19K |
| Western Europe | ~16K |
| Sub-Saharan Africa | ~16K |
| Southeast Asia | ~11K |
| Central America & Caribbean | ~10K |
| Eastern Europe | ~5K |

### Takeaways

- The **2010s** have the highest number of recorded incidents, with the yearly peak at roughly **16.9K attacks**.
- **Middle East & North Africa** and **South Asia** together account for over half of all recorded attacks.
- Most attacks fall into the **Medium** and **Low** severity categories; only about 10% are **High** severity.
- The vast majority of recorded attacks are classified as successful.
- On average, an attack results in about **5.18 casualties** (killed + wounded).

---

## 📐 Power BI Model & DAX

The dashboard is built on the `vw_gtd_analysis` view from PostgreSQL, plus a dedicated `DateTable`.

### Total Attacks

```DAX
Total Attacks =
DISTINCTCOUNT('public vw_gtd_analysis'[eventid])
```

### Total Killed

```DAX
Total Killed =
SUM('public vw_gtd_analysis'[killed])
```

### Total Wounded

```DAX
Total Wounded =
SUM('public vw_gtd_analysis'[wounded])
```

### Total Casualties

```DAX
Total Casualties =
SUM('public vw_gtd_analysis'[total_casualties])
```

### Average Casualties per Attack

```DAX
Avg Casualties per Attack =
DIVIDE(
    [Total Casualties],
    [Total Attacks],
    0
)
```

### Success Rate

```DAX
Success Rate =
DIVIDE(
    CALCULATE(
        [Total Attacks],
        'public vw_gtd_analysis'[success] = 1
    ),
    [Total Attacks],
    0
)
```

> Adjust the `success` comparison (`1` vs `"1"`) to match the column's data type in your model.

### Date Table

The `DateTable` contains `Date`, `Year`, `Month Number`, `Month Name`, `Month Year`, and `Month Year Sort`. `Month Year` is sorted by `Month Year Sort` so visuals show months in chronological order.

---

## ⚠️ Data Limitations

- Some records contain unknown or missing values.
- Casualty values may be incomplete for some events.
- Reporting and recording practices vary across countries and years.
- The dataset version used covers 1970–2017 only.
- One malformed CSV record was excluded during import.

Results describe the **recorded dataset**, not a complete picture of all terrorism incidents worldwide.

---

## 🚀 Future Improvements

- Terrorist group trend analysis
- Weapon and target type analysis
- Year-over-year regional comparison
- Additional dashboard pages with drill-through
- Automated ETL pipeline
- Statistical analysis and predictive modeling in Python

---

## 👨‍💻 Author

**Sabbir Hossain**
Aspiring Data Analyst | BI Engineer

- LinkedIn: [sabbir-hossain-2001da](https://www.linkedin.com/in/sabbir-hossain-2001da)
- GitHub: [SABBIR-HOSSAIN-001](https://github.com/SABBIR-HOSSAIN-001)

*Built as a portfolio project to demonstrate end-to-end data analytics skills: Python → PostgreSQL → SQL → Power BI.*
