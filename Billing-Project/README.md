# Agent Billing & Compliance Dashboard | Power BI

> **Production Power BI billing analytics solution delivered as IT Analyst — full 2025 billing data audit & correction + agent productivity tracking system for an energy company's billing operations**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX Studio](https://img.shields.io/badge/DAX%20Studio-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

---

## 📊 Business Problem

An energy utility company managed billing for a team of 27+ agents processing transactions monthly. Before this solution existed, the organization faced two critical and compounding problems:

**1. Corrupted billing data across all of 2025**
The full year's billing records contained financial inconsistencies and calculation errors that made it impossible to reliably assess agent output or cost efficiency. There was no audited, trustworthy dataset to work from.

**2. Zero visibility into agent billing productivity**
Management had no way to see — in monetary terms — what each agent was actually producing relative to their salary. There was no tool to:
- Compare individual agent salary against their transaction cost output
- Track whether agents were meeting monthly productivity targets
- Identify high vs. low performers based on cost-efficiency
- Review billing performance split by on-site vs. virtual transactions

**Impact:** Monthly billing reviews were manual, time-consuming, and unreliable — built on data nobody could fully trust.

---

## 💡 Solution Overview

Delivered a **3-view Power BI billing dashboard** in 1–2 weeks that solved both problems simultaneously: first by auditing and correcting the entire 2025 billing dataset, then by building a production-ready analytics tool now used every monthly billing cycle.

### Dashboard Views
- **Agent Summary Dashboard** — Full agent ranking by salary, transaction cost, difference, and compliance %
- **Target Dashboard** — Monthly point achievement vs. goals, segmented by Team 1 and Team 2
- **Agent Detail Dashboard** — Per-agent drill-down into transaction cost by process classification and type

### Key Features
- **Salary vs. Output Comparison:** See exactly what each agent costs vs. what they produce in billable transactions
- **Compliance Rate Tracking:** Dynamic % compliance per agent with period-over-period trend alerts
- **Team Segmentation:** Separate views for Team 1 (25 agents) and Team 2 (5 agents) with individual goals
- **Point Achievement System:** Monthly targets tracked with achieved level scoring per agent
- **On-site vs. Virtual Split:** Transaction breakdown by channel per agent
- **Agent Detail Drill-down:** Agile vs. Non-Agile classification with per-process-type unit cost breakdown
- **Conditional Formatting:** Instant visual identification of top performers and underperformers

---

## 📈 Key Metrics

| Metric | Value | Description |
|--------|-------|-------------|
| **Agents Tracked** | 27 | Full billing team covered |
| **Total Salary Pool** | $1.47B+ | Combined monthly salary across all agents |
| **Total Transaction Cost** | $877M+ | Aggregated billable output |
| **Avg. Compliance Rate** | 59.72% | Overall team billing compliance |
| **Top Performer** | 75.25% | Highest individual compliance rate |
| **Period Trend** | -9.65% | Compliance drop vs. prior period — flagged for management |
| **Dev to Production** | 1–2 Weeks | Solo delivery timeline |

---

## 🔍 Key Insights & Findings

### 1. Compliance Gap Across the Team
**Finding:** Average compliance of 54.21% with a -9.65% drop from the prior period  
**Insight:** Team-wide performance decline, not isolated to individual agents  
**Action:** Triggered management review of workload distribution and process bottlenecks

### 2. Wide Performance Spread
**Finding:** 38-point gap between top (75.25%) and bottom (36.82%) performers  
**Opportunity:** Significant coaching and standardization potential  
**Value:** Bringing bottom quartile to median compliance would measurably reduce cost-per-transaction

### 3. Salary-Cost Delta as Efficiency Indicator
**Finding:** Top agent (Lucia Esperanza) generated $40.9M in transaction cost vs. $54.4M salary — a $13.4M difference  
**Insight:** Delta size directly measures productivity efficiency per agent  
**Value:** First time management could see this comparison in real time

### 4. Team 2 Underperformance
**Finding:** Team 2 total point deficit of -$50.9K against combined $149.5K goal  
**Insight:** Team 2 is structurally underperforming against targets, not just individual agents  
**Action:** Separate team view enables targeted intervention without noise from Team 1 data

### 5. Process Classification Breakdown (Agent Detail)
**Finding:** Agile processes (1,074 pts, $28.5M) and Non-Agile (1,072 pts, $29.1M) are nearly equal in volume  
**Insight:** Balanced workload distribution, but unit cost differences by process type reveal efficiency gaps  
**Opportunity:** High-cost process types (e.g., Temporary Separation: $2.49M, 97 pts) are prime optimization targets

---

## 🛠️ Technical Implementation

### Technology Stack
| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard design, interactivity, conditional formatting |
| **DAX** | Compliance %, salary-cost delta, point achievement measures |
| **Power Query (M)** | ETL, billing record audit & correction, column derivations |
| **DAX Studio** | Query optimization, measure validation, performance tuning |

### Data Architecture

```
Fact Tables:
├── Billing Records (full 2025 — audited & corrected)
│   ├── Agent ID, Period, Transaction Cost
│   ├── Unit Points, Classification (Agile / Non-Agile)
│   └── Process Type, Channel (On-site / Virtual)
│
└── Targets
    ├── Agent ID, Monthly Goal
    └── Team Assignment (Team 1 / Team 2)

Dimension Tables:
├── Agents
│   └── Agent ID, Full Name, Team
│
├── Process Classification
│   └── Classification ID, Name, Category
│
└── Time
    └── Period, Month, Year
```

### Key DAX Measures

**Compliance Rate:**
```dax
Avg Compliance = 
DIVIDE(
    [Total Transaction Cost],
    [Total Salary]
)
```

**Salary vs. Cost Difference:**
```dax
Diferencia1 = [Salario] - [Total Costo Unitario]
```

**Dynamic Month Filtering (Billing Comparison):**
```dax
Procesos_Mes1 = 
CALCULATE(
    COUNTROWS('MESES'),
    FILTER(
        'MESES',
        FORMAT('MESES'[FECHA REGISTRO DEL PROCESO], "YYYY-MM") = 
        SELECTEDVALUE(MesesDisponibles[Mes])
    )
)
```

*See [DAX-Measures.md](DAX-Measures.md) for the complete measure library with business context*

### Data Quality Work
Before a single visual was built, the full 2025 billing dataset was audited and corrected:
- Cross-referenced transaction records against source billing system
- Corrected unit cost calculation errors across all agent records
- Validated agent assignments and process type classifications
- Established a clean, reliable foundation for all downstream analytics

---

## 📸 Dashboard Screenshots

### Agent Summary Dashboard
![Agent Summary](screenshots/agent_summary.png)
*Full agent ranking by Total Salary, Transaction Cost, Difference, and Avg. Compliance % — overall 54.21% compliance with -9.65% period trend*

### Target Dashboard — Team 1 & Team 2
![Target Dashboard](screenshots/target_dashboard.png)
*Monthly point achievement vs. goals per agent, segmented by team — Team 2 showing -$50.9K point deficit*

### Agent Detail Dashboard
![Agent Detail](screenshots/agent_detail.png)
*Per-agent drill-down into Agile vs. Non-Agile transaction cost and unit points by process type*

---

## 📁 Repository Structure

```
FlyAnalytics-Billing-Dashboard/
├── README.md                        # This file
├── DAX-Measures.md                  # Full DAX measure library with business context
├── Documentation/
│   └── Case-Study.pdf               # Full project case study
└── Screenshots/
    ├── agent_summary.png
    ├── target_dashboard.png
    └── agent_detail.png
```

---

## ⏱️ Project Timeline

**Duration:** 1–2 Weeks (Data Audit → Production Deployment)  
**Role:** IT Analyst  
**Delivery Model:** Solo delivery — requirements, data correction, development, and deployment

| Phase | Focus | Deliverables |
|-------|-------|--------------|
| **Phase 1** | Data Audit & Correction | Full 2025 billing dataset reviewed, errors corrected, validated |
| **Phase 2** | Dashboard Development | 3-view Power BI solution built, optimized, and deployed to production |

---

## 🎯 Business Impact

| Area | Before | After |
|------|--------|-------|
| **Billing Data Quality** | 2025 records had errors & inconsistencies | Full year audited, corrected & validated |
| **Agent Productivity Visibility** | No monetary view of agent output | Real-time salary vs. transaction cost per agent |
| **Monthly Reporting** | Manual, time-consuming process | Dashboard updated each billing cycle |
| **Performance Management** | No compliance benchmark | 54.21% avg tracked with trend alerts |
| **Target Tracking** | No goal measurement system | Point-based targets with team segmentation |
| **Decision Making** | Reactive, based on incomplete data | Proactive, data-driven management reviews |

---

## 🚀 Skills Demonstrated

**Technical**
- Power BI dashboard design and multi-view architecture
- DAX for compliance metrics, salary-cost deltas, and dynamic filtering
- Power Query (M) for ETL and large-scale data correction
- DAX Studio for performance optimization
- Financial data auditing and validation

**Business**
- Translating billing operations into actionable KPIs
- Data quality assessment and remediation
- Stakeholder-ready dashboard design
- Cost-efficiency analysis and performance benchmarking

---

## 📝 License & Usage

This project represents real work delivered as IT Analyst for an energy company's billing operations. The dashboard architecture, DAX logic, data model, and analytical approach are original work developed and deployed to production.

**Portfolio Version:** All agent names, financial figures, and operational data have been fully anonymized and modified to protect client confidentiality. The methodology, technical implementation, and business logic accurately reflect the production solution.

---

## 🔗 Additional Resources

- **Full Case Study (PDF):** [View detailed case study](Documentation/Case-Study.pdf)
- **DAX Measures:** [View complete measure library](DAX-Measures.md)
- **LinkedIn:** [linkedin.com/in/jebarrioscornett](https://linkedin.com/in/jebarrioscornett)

---

*Last Updated: March 2026*
