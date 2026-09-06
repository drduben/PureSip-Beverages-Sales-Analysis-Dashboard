# 🥤 PureSip Beverages — Sales Analysis Dashboard

**A Distribution & Retail Analytics Case Study | Power BI (Folder Connector, Automated Refresh & DAX)**

![Tools](https://img.shields.io/badge/Tool-Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Domain](https://img.shields.io/badge/Domain-Beverage%20Distribution-6c4fa1)
![Type](https://img.shields.io/badge/Project-Case%20Study-orange)

> Case study built for **PureSip Beverages**, a beverage distributor supplying major retail chains, to replace siloed, manually-consolidated regional spreadsheets with a single automated Power BI data pipeline and sales dashboard.

📊 **Dashboard preview:**
![PureSip Sales Analysis Dashboard](PureSip_Sales_Analysis_Dashboard.png)

---

## 📌 Project Overview

| | |
|---|---|
| **Client** | PureSip Beverages — a distributor of major beverage brands (Coca-Cola, Diet Coke, Sprite, Fanta, Powerade, Dasani Water) supplying retail chains including Walmart, Costco, Walgreens, and Target |
| **Role** | Data Analyst |
| **Tool Used** | Power BI Desktop — **Folder connector** for automated multi-file ingestion, Power Query, DAX measures |
| **Reporting Period** | Full year 2022 |
| **Data Scope** | 288 transaction records consolidated from 4 separate retailer spreadsheets, covering 4 retailers, 6 beverage brands, and 3 U.S. regions |

## 🎯 The Business Problem

PureSip relied on **individual spreadsheets maintained by each regional manager** to track sales, uploaded separately for each retailer relationship. This siloed setup created three core problems:

- **Data consolidation overhead** — manually merging spreadsheets from each region for company-wide reporting was slow and error-prone
- **Data accuracy risk** — inconsistent formats and entry practices across locations increased the chance of inaccurate reporting
- **Limited analysis capability** — spreadsheets offered no real trend analysis or cross-location performance comparison

## 🛠️ The Solution: Power BI Folder Connection

Rather than manually copying and pasting data between files, this project used **Power BI's local folder connector** to solve the consolidation problem at the source:

1. A **shared folder** was set up on a central server, accessible to all retailers
2. Each retailer/regional manager **uploads their own sales spreadsheet** to this folder at the end of each reporting period
3. Power BI connects directly to the **folder** (not a single file) and **automatically combines every spreadsheet inside it into one unified table** — `PureSip Data Folder` — using Power Query
4. Because the connection targets the folder itself, the model **refreshes automatically** whenever a new or updated spreadsheet is dropped in, with zero manual re-consolidation

This is the core technical skill this case study demonstrates: building a **scalable, self-updating data pipeline** rather than a one-off static import — the model would keep working unchanged even if PureSip added a fifth, sixth, or tenth retailer.

### Data Model & DAX Measures

The consolidated table (`PureSip Data Folder`, 288 rows) includes: Retailer, Contact, Retailer ID, Order Date, Payment Date, Payment Period, Region, State, Beverage Brand, Price per Unit, Units Sold, and Sales.

```DAX
Total Sales      = SUM('PureSip Data Folder'[Sales])
Total Qty Sold    = SUM('PureSip Data Folder'[Units Sold])
No of Retailers   = DISTINCTCOUNT('PureSip Data Folder'[Retailer ID])
Target            = 250000
Total Sales Display   = FORMAT([Total Sales], "$#,##0")
Total Qty Sold Display = FORMAT([Total Qty Sold], "#,##0")
```

## 📊 The Dashboard

### Headline KPIs

| Metric | Value |
|---|---|
| Total Sales | **$1,213,018** |
| Total Quantity Sold | **2,309,850 units** |
| Number of Retailers | **4** |
| KPI Tracker (single-contact view) | **$238.85K vs. $250K target (–4.46%)** |

### Visuals included

1. **KPI Tracker | Contact** — a gauge-style card tracking one regional contact's sales against a fixed $250,000 target, defaulting to contact *Stuart* (Target), currently **4.46% below target**
2. **Sales | Month Analysis** (bar/trend chart) — monthly sales across 2022, with August highlighted as the peak month
3. **Sales | Regional Analysis** (map) — sales by U.S. region/state
4. **Sales | Retailer Analysis** (bar chart) — sales by retail chain
5. **Sales | Brand Analysis** (bar chart) — sales by beverage brand
6. **Beverage Brand / Contact slicers** — interactive filtering across the whole report

## ✅ Key Business Questions — Answered

| Question | Answer |
|---|---|
| What is the overall sales trend across the year? | Sales grow steadily from a **January low of $82,063** to a **peak of $115,950 in August**, before easing slightly into Q4 ($105,600–$115,300) — a roughly 41% increase from the year's lowest to highest month, with no sharp seasonal collapse |
| Which retailer generates the most sales? | **Walmart** leads with **$391,768**, followed by **Costco** ($331,750), **Walgreens** ($250,650), and **Target** ($238,850) |
| Which beverage brand performs best? | **Dasani Water** leads at **$233,775**, narrowly ahead of **Coca-Cola** ($228,445) and **Diet Coke** ($214,363); **Fanta** is the lowest performer at **$166,550** |
| How does performance vary by region? | **West (California)** dominates at **$582,400** — nearly 1.5x the next region — followed by **Northeast (New York)** at **$391,768** and **South (Texas)** at **$238,850** |
| How is an individual account tracking against target? | The built-in KPI tracker shows contact **Stuart (Target retailer)** at **$238,850 against a $250,000 target — 4.46% under goal**, giving PureSip a way to monitor individual regional manager performance directly inside the report |
| How many retail partners does PureSip currently supply? | **4** — Walmart, Costco, Walgreens, and Target |

## 🔍 Key Insights

- **Walmart is PureSip's most valuable retail partner** by revenue ($391,768) but not by volume — Walmart also moves the most units (706,600), meaning its per-unit pricing runs slightly below some competitors, consistent with a large-scale retail buyer.
- **Water and diet cola are punching above their category weight**: Dasani Water leads all brands in revenue despite Coca-Cola and Diet Coke moving more comparable volumes, likely reflecting Dasani's higher average price per unit (~$0.59 vs. Coca-Cola's ~$0.48) — a useful signal for margin-focused brand prioritization.
- **Sales are heavily geographically concentrated**: California (West) alone accounts for **48% of total company sales**, more than New York and Texas combined — a strong signal that West Coast retail relationships are disproportionately important to PureSip's business.
- **Payment terms are mostly consistent but not always honored**: the majority of transactions were paid within the standard 30-day period, but payment lag stretched as long as **65 days** in some cases — worth flagging for accounts-receivable follow-up with slower-paying retailers.
- **August is the clear seasonal peak** ($115,950), likely tied to back-to-school and late-summer demand, while January and February are the softest months — useful for planning inventory and promotional timing.
- **The automated folder-connection architecture itself is a key insight**: by connecting to a folder instead of a single file, PureSip's data pipeline scales automatically as new retailers or reporting periods are added, with no rework required — directly solving the original "siloed spreadsheet" problem at its root.

## 💡 Recommendations

1. **Investigate Target's underperformance against its $250K benchmark** — a 4.46% shortfall flagged directly by the KPI tracker, worth a closer look at what's driving it (pricing, assortment, promotional support).
2. **Double down on West Coast / California relationships**, given they account for nearly half of total sales — consider whether this concentration is an opportunity to expand further or a risk worth diversifying against.
3. **Review brand-level pricing strategy** — Dasani Water's higher price point delivering the top revenue result suggests there may be room to test pricing on other high-volume, lower-margin brands like Coca-Cola.
4. **Formalize payment-term enforcement** with retailers exceeding the standard 30-day payment window to protect cash flow.
5. **Extend the folder-connection model to additional data sources** (e.g. marketing spend, inventory) now that the automated refresh pipeline is proven, to build a more complete view of the business without added manual work.

## 🛠️ Skills Demonstrated

`Power BI` · `Folder Connector / Automated Data Refresh` · `Power Query` · `DAX Measures` · `KPI Tracking & Target Analysis` · `Geospatial Visualization` · `Distribution & Retail Analytics` · `Business Insight Generation`

## 📁 Repository Contents

- `PureSip_Sales_Analysis_Dashboard.pbix` — full Power BI file (folder-connected data model, DAX measures, dashboard)
- `PureSip_Sales_Analysis_Dashboard.png` — dashboard screenshot
- `PureSip_Beverages_Case_Study_Brief.docx` — original project brief
- `README.md` — this write-up

---

*Case study based on the PureSip Beverages project brief. #PowerBI #DataAnalytics #DAX #RetailAnalytics*
