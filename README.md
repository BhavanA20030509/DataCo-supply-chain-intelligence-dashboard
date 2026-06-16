# DataCo Supply Chain Intelligence Dashboard 📦

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Data Analytics](https://img.shields.io/badge/Data%20Analytics-0F6E56?style=for-the-badge)
![Supply Chain](https://img.shields.io/badge/Supply%20Chain-E24B4A?style=for-the-badge)

> A single-page Power BI dashboard analyzing 180,519 real-world supply chain orders 
> across 5 global markets — uncovering revenue performance, delivery failures, 
> profit drivers, and fraud risk in one view.



## 📌 Project Objective

Most supply chain reports tell you what happened.
This dashboard tells you **why it happened** and **what to do about it.**

Built to answer 4 core business questions:
- 👉 Which markets and products are driving revenue?
- 👉 Is the supply chain actually delivering on time?
- 👉 Where is profit being made — and destroyed?
- 👉 Where is fraud and delivery risk concentrated?

---

## 📊 Dataset

| Property | Details |
|----------|---------|
| **Source** | DataCo Global Supply Chain Dataset (Kaggle) |
| **Rows** | 180,519 orders |
| **Columns** | 53 features |
| **Period** | January 2015 — February 2018 |
| **Markets** | Europe, LATAM, Pacific Asia, USCA, Africa |
| **File** | `DataCoSupplyChainDataset.csv` |

### Key columns used:
- `Sales` — order revenue
- `Order Profit Per Order` — profit per transaction
- `Delivery Status` — on time / late / advance / canceled
- `Late_delivery_risk` — binary risk flag (0/1)
- `Order Status` — COMPLETE, CANCELED, SUSPECTED_FRAUD etc.
- `Department Name` — product department
- `Shipping Mode` — Standard / First / Second / Same Day
- `Market` — geographic market
- `Product Name` — product catalog
- `Order Item Discount Rate` — discount applied
- `Type` — payment method
- `order date (DateOrders)` — transaction date

---

## 🛠 Tools & Techniques

| Tool / Technique | Purpose |
|-----------------|---------|
| **Power BI Desktop** | Dashboard development |
| **DAX Measures** | KPI calculations |
| **Custom Date Table** | Time intelligence |
| **Conditional Formatting** | Dynamic color coding |
| **Matrix Heatmap** | Profit by dept × shipping |
| **Top N Filter** | Top 8 products |
| **Calculated Columns** | SWITCH for label cleanup |
| **Multi-color Formatting** | Per-category bar colors |

---

## 📐 DAX Measures Written

```dax
-- Total Revenue
Total Revenue = SUM(DataCoSupplyChainDataset[Sales])

-- Total Profit
Total Profit = SUM(DataCoSupplyChainDataset[Order Profit Per Order])

-- Total Orders
Total Orders = COUNTROWS(DataCoSupplyChainDataset)

-- On Time Delivery %
On Time Delivery % = 
DIVIDE(
    COUNTROWS(FILTER(
        DataCoSupplyChainDataset,
        DataCoSupplyChainDataset[Delivery Status] = "Shipping on time"
    )),
    COUNTROWS(DataCoSupplyChainDataset)
)

-- Late Delivery Risk %
Late Delivery Risk % = 
DIVIDE(
    COUNTROWS(FILTER(
        DataCoSupplyChainDataset,
        DataCoSupplyChainDataset[Late_delivery_risk] = 1
    )),
    COUNTROWS(DataCoSupplyChainDataset)
)

-- Fraud Flagged %
Fraud Flagged % = 
DIVIDE(
    COUNTROWS(FILTER(
        DataCoSupplyChainDataset,
        DataCoSupplyChainDataset[Order Status] = "SUSPECTED_FRAUD"
    )),
    COUNTROWS(DataCoSupplyChainDataset)
)

-- Profit Margin %
Profit Margin % = 
DIVIDE(
    SUM(DataCoSupplyChainDataset[Order Profit Per Order]),
    SUM(DataCoSupplyChainDataset[Sales])
)

-- Avg Profit Per Order
Avg Profit Per Order = 
AVERAGE(DataCoSupplyChainDataset[Order Profit Per Order])

-- Avg Discount Rate
Avg Discount Rate = 
AVERAGE(DataCoSupplyChainDataset[Order Item Discount Rate])

-- Fraud Order Count
Fraud Order Count = 
COUNTROWS(FILTER(
    DataCoSupplyChainDataset,
    DataCoSupplyChainDataset[Order Status] = "SUSPECTED_FRAUD"
))
```
---

## 📈 Key Insights

### Revenue & Profit
- Total revenue of **$36.78M** across 181K orders with **$3.97M profit**
- Profit margin of **10.8%** — acceptable but impacted by heavy discounting
- **Europe and LATAM** are the top revenue markets

### Delivery Performance 🚨
- Only **17.84%** of orders delivered on time — industry benchmark is **95%**
- **54.83%** of all orders carry a late delivery risk
- Nearly **99,000 orders** at risk of late delivery out of 181K total

### Product Performance
- **Field & Stream, Perfect Rip Deck, Diamondback** are top revenue products
- Classic **Pareto 80/20 pattern** — small number of products drive majority of revenue
- These top products need highest stock and shipping priority

### Profit by Department & Shipping
- **Technology** generates highest avg profit per order ($75–$82)
- **Same Day shipping** reduces profit margin across almost every department
- **Pet Shop and Book Shop** with Same Day shipping near zero or negative margin

### Fraud & Risk
- **2.25%** of orders flagged as SUSPECTED_FRAUD (2,166 orders)
- **LATAM** leads in fraud order count despite being 2nd highest revenue market
- **Heavy discounting** directly correlates with lower profit margins

---

## 🚨 Business Risks Identified

| Risk | Severity | Market/Area Affected |
|------|----------|---------------------|
| 17.84% on-time delivery rate | 🔴 Critical | All markets |
| LATAM high fraud concentration | 🔴 High | LATAM |
| Discount rate eroding margins | 🟡 Medium | All departments |
| Revenue concentrated in few products | 🟡 Medium | All markets |
| Same Day shipping unprofitable | 🟡 Medium | Pet Shop, Book Shop, Golf |

---

## 📝 Business Recommendations

1. **Fix delivery logistics urgently** — 17.84% on-time rate will drive customer churn at scale
2. **Implement fraud controls for LATAM** — highest fraud volume in highest-risk revenue market
3. **Cap discount rates above 15%** — data shows these consistently produce near-zero margins
4. **Prioritize top 8 products** for stock reliability and shipping performance
5. **Reprice or limit Same Day shipping** for low-margin departments
6. **Diversify product revenue** — reduce dependency on small number of top SKUs

---

## 📁 Repository Structure

---

## 📋 Dashboard Layout
---

## 🚀 How to Run This Project

1. **Clone this repository**
```bash
git clone https://github.com/BhavanA20030509/DataCo-Supply-Chain-Dashboard.git
```

2. **Download Power BI Desktop**
   - Free download at [powerbi.microsoft.com](https://powerbi.microsoft.com)

3. **Open the dashboard**
   - Open `SupplyChainDashboard.pbix` in Power BI Desktop

4. **Connect the dataset**
   - If prompted, point the data source to `DataCoSupplyChainDataset.csv`
   - Click Refresh

5. **Explore the dashboard**
   - All charts, measures and formatting load automatically

---

## 💡 Key Learning

Supply chain dashboards don't just track deliveries.
They expose the hidden link between operational decisions and financial outcomes.

Every late delivery is a customer relationship at risk.
Every fraudulent order is revenue that never arrives.
Every discount is a margin decision multiplied across thousands of orders.

**Data makes invisible patterns visible — and visible patterns drive better decisions.**

---

## 🙋 About Me

**Bhavana R**
Aspiring Data Analyst | Power BI | SQL | Python

---

## ⭐ If you found this project useful, please star the repository!
