# 🌍 Global Terrorism Analysis

An end-to-end Business Intelligence project that analyzes the **Global Terrorism Database (GTD)** using **Python, PostgreSQL, SQL and Power BI**, and presents the findings in an interactive dashboard.

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-025E8C?logo=databricks&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)

---

## 🧭 What This Project Does

| Icon | Task | What was done |
|:---:|---|---|
| 🐍 | **Data Loading** | Loaded the GTD data using a Python notebook |
| 🗄️ | **Data Storage** | Stored the data in a PostgreSQL database |
| 🔎 | **Data Analysis** | Wrote SQL queries to explore and summarize the data |
| 📊 | **Dashboard** | Built an interactive Power BI dashboard (Global Overview page) |
| 🎛️ | **Interactivity** | Added slicers for Decade, Year, Country and Attack Type, plus a Reset button |
| 📝 | **Documentation** | Documented the project in this README |

---

## 📑 Table of Contents

- [Dashboard Preview](#-dashboard-preview)
- [Project Overview](#-project-overview)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
- [Author](#-author)

---

## 📊 Dashboard Preview

![Global Terrorism Overview Dashboard](powerbi/screenshots/Screenshot_power_bi.png)

### Dashboard at a Glance

| KPI | Value |
|---|---:|
| 💥 Total Attacks | 171K (171,055) |
| ☠️ Total Killed | 386K |
| 🩹 Total Wounded | 500K |
| 📉 Avg Casualties per Attack | 5.18 |

### 📈 Visuals on the Global Overview Page

- 🗺️ **Global Terrorist Attacks by Country:** filled map showing attack intensity by country
- 🍩 **Attack Severity Distribution:** donut chart (Low / Medium / High)
- 📅 **Global Terrorist Attacks, Yearly Trend:** line chart of attacks per year
- 🌐 **Attacks by Region:** ranked bar chart of attack counts per region

### 🎛️ Interactive Controls

- Select Decade
- Select Year (range slider, 1970–2017)
- Select Country
- Select Attack Type
- Reset button to clear all filters

---

## 📌 Project Overview

This project analyzes the Global Terrorism Database (GTD), maintained by START at the University of Maryland, to answer questions such as:

- How did terrorism incidents change over time?
- Which countries and regions were most affected?
- Which attack types were most common?
- How severe were attacks in terms of people killed and wounded?

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| 🐍 Python | Loading the GTD data |
| 🐘 PostgreSQL | Storing and querying the data |
| 🧾 SQL | Data exploration and aggregation |
| 📊 Power BI | Interactive dashboard and visualization |

---

## 📂 Project Structure

```
Global-Terrorism-Analysis/
├── data/
│   └── data_loading_by_python.ipynb
├── powerbi/
│   ├── screenshots/
│   │   └── Screenshot_power_bi.png
│   └── Global_Terrorism_Analysis_BI.pbix
├── sql/
│   └── sql_raw.txt
└── README.md
```

| Path | Description |
|---|---|
| [`data/data_loading_by_python.ipynb`](data/data_loading_by_python.ipynb) | Python notebook for loading the data |
| [`sql/sql_raw.txt`](sql/sql_raw.txt) | SQL queries used for analysis |
| [`powerbi/Global_Terrorism_Analysis_BI.pbix`](powerbi/Global_Terrorism_Analysis_BI.pbix) | Power BI dashboard file |
| [`powerbi/screenshots/`](powerbi/screenshots/) | Dashboard screenshots |

---

## 🚀 How to Use

1. **Clone the repository**
   ```bash
   git clone https://github.com/SABBIR-HOSSAIN-001/Global-Terrorism-Analysis.git
   ```
2. **Load the data:** run the notebook in the `data/` folder.
3. **Run the queries:** use the SQL in `sql/sql_raw.txt` against your PostgreSQL database.
4. **Explore the dashboard:** open `powerbi/Global_Terrorism_Analysis_BI.pbix` in Power BI Desktop.

---

## 👤 Author

**Sabbir Hossain**, Aspiring Data Analyst | BI Engineer

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sabbir-hossain-2001da)
[![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/SABBIR-HOSSAIN-001)

---

⭐ If you found this project useful, consider giving it a star!
