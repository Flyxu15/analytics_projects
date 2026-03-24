# analytics_projects

> Collection of Power BI analytics solutions delivered as IT Analyst — production dashboards for billing operations and customer service management at an energy utility company

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

---

## 📂 Projects Overview

This repository showcases two enterprise-grade Power BI analytics solutions deployed to production and actively used for operational decision-making at an energy company. Both projects demonstrate end-to-end BI development: from data auditing and ETL through advanced DAX calculations to interactive dashboard design.

### [🧾 Billing-Project](./Billing-Project)
**Agent Billing & Compliance Dashboard**

Full 2025 billing data audit and agent productivity tracking system monitoring 27+ agents across $1.47B+ salary pool.

**Key Metrics:**
- 27 agents tracked across multiple teams
- $877M+ total transaction cost processed
- 59.72% average compliance rate
- 1-2 week development to production timeline

**Core Features:**
- Salary vs. transaction cost comparison per agent
- Real-time compliance rate tracking with period-over-period trends
- Monthly point achievement system with team segmentation
- Agile vs. Non-Agile process classification breakdown
- Agent detail drill-down by process type and channel

**Tech Highlights:**
- Data quality remediation: Full 2025 billing dataset audit and correction
- Advanced DAX: Safe division patterns, SUMX for row-level accuracy, disconnected tables for dynamic period filtering
- Performance optimization: DAX Studio analysis and query tuning

---

### [📊 Productivity-Project](./Productivity-Project)
**Customer Service Analytics Dashboard**

Comprehensive 13-page operational analytics platform tracking service levels, agent performance, and process management across 28,000+ tickets.

**Key Metrics:**
- 28,000+ customer service tickets analyzed
- 75,000+ process records tracked
- 60+ agents monitored across multiple regions
- 36.82% service level compliance (15-minute SLA target)

**Core Features:**
- Multi-level service tracking: wait time and service time SLA monitoring
- Peak hours analysis for optimal staffing decisions
- Month-over-month comparison across services, groups, and process types
- Agent productivity ranking and performance spread analysis
- Customer satisfaction tracking: 187,687 survey responses, 99.1% approval rate

**Tech Highlights:**
- Complex time intelligence: Dynamic month filtering with disconnected tables
- Star schema data model integrating tickets, agents, services, and processes
- Custom DAX measures for datetime calculations and working day adjustments
- Conditional formatting for instant visual performance identification

---

## 🛠️ Technical Skills Demonstrated

### Power BI Development
- Multi-page dashboard architecture with consistent navigation
- Interactive filtering with drill-through actions and bookmarks
- Conditional formatting for performance indicators
- Data modeling with star schema and proper relationships

### DAX Expertise
- **Time Intelligence:** Month-over-month comparisons, dynamic period filtering, working day calculations
- **Advanced Functions:** CALCULATE, FILTER, AVERAGEX, SUMX, DIVIDE, SELECTEDVALUE, FORMAT
- **Context Manipulation:** Understanding filter context, using ALL() and VALUES()
- **Variables:** Performance optimization and code clarity
- **Measure Chaining:** Building complex metrics from base measures

### Power Query (M)
- ETL processes for data transformation and cleaning
- Large-scale data audit and correction workflows
- Column derivations and calculated fields
- Data type conversions and date formatting

### Performance Optimization
- DAX Studio for query plan analysis
- Identifying and eliminating storage engine bottlenecks
- Optimizing measure calculations for faster load times
- Pre-calculated columns vs. runtime measures trade-offs

### Business Intelligence
- Translating business requirements into technical solutions
- KPI design and metric definition
- Data quality assessment and remediation
- Stakeholder-ready visualization design

---

## 📈 Business Impact

Both projects solved critical operational visibility gaps and transformed manual, error-prone processes into reliable, data-driven management tools:

| Impact Area | Billing Project | Productivity Project |
|-------------|-----------------|---------------------|
| **Data Quality** | Full 2025 billing dataset audited and corrected | Centralized 28K+ tickets from disparate sources |
| **Visibility** | First-ever salary vs. output comparison per agent | Real-time SLA compliance across 60+ agents |
| **Decision Making** | Data-driven performance reviews and coaching | Optimal staffing decisions based on peak hour analysis |
| **Efficiency** | Automated monthly billing reviews | Eliminated days-long manual reporting processes |
| **Accountability** | Point-based target tracking with team segmentation | Individual agent performance benchmarking |

---

## 📁 Repository Structure

```
analytics_projects/
├── README.md                          # This file
├── Billing-Project/
│   ├── README.md                      # Detailed billing project documentation
│   ├── DAX-Measures.md                # Complete DAX measure library with context
│   ├── Documentation/
│   │   └── Billing_CaseStudy.pdf      # Full case study with screenshots
│   └── Screenshots/
│       ├── agent_summary.png
│       ├── target_dashboard.png
│       └── agent_detail.png
└── Productivity-Project/
    ├── README.md                      # Detailed productivity project documentation
    ├── DAX-Measures.md                # Complete DAX measure library with context
    ├── Documentation/
    │   └── CaseStudy_Productivity.pdf # Full case study with screenshots
    └── Screenshots/
        ├── home_dashboard.png
        ├── peak_hours.png
        ├── agents.png
        └── [8 additional dashboard views]
```

---

## 🎯 Project Highlights

### Billing Project
- **Problem Solved:** Corrupted 2025 billing data + zero visibility into agent productivity
- **Solution:** 1-2 week delivery from data audit to production deployment
- **Impact:** Management can now see exactly what each agent produces vs. their cost
- **Technical Achievement:** Safe division patterns, row-level accuracy with SUMX, disconnected tables for arbitrary month comparisons

### Productivity Project
- **Problem Solved:** No centralized system to measure agent productivity across 60+ agents
- **Solution:** 1-month agile development of 13-page comprehensive analytics platform
- **Impact:** Primary tool for daily operations monitoring and staffing decisions
- **Technical Achievement:** Complex time intelligence, working day calculations, dynamic filtering across 28K+ tickets

---

## ⏱️ Development Timeline

**Billing Project:** 1-2 Weeks
- Week 1: Data audit, ETL, and corrections across full 2025 billing dataset
- Week 1-2: Dashboard development (3 views), DAX optimization, production deployment

**Productivity Project:** 1 Month
- Week 1: Stakeholder interviews, requirements, data model design
- Week 2: Core dashboards (Home, Peak Hours, Agents, Groups)
- Week 3: Advanced analytics (Processes, SLA tracking, comparative views)
- Week 4: DAX Studio optimization, UAT, production deployment

---

## 🚀 Key Learnings

### Data Quality First
Both projects reinforced that trustworthy analytics require a clean, validated data foundation. The billing project's data audit phase was critical to ensuring every downstream metric was reliable.

### Monetary KPIs Drive Action
Translating performance into financial terms (salary vs. transaction cost) made insights immediately actionable for management—far more impactful than abstract scores.

### Segmented Views Scale Better
Building separate views for different user personas (executive oversight vs. individual agent tracking) meant one tool could serve multiple audiences effectively.

### DAX for Dynamic Calculations
Building metrics as dynamic DAX measures rather than static calculated columns ensured dashboards stayed accurate as new data loaded each cycle.

### Performance Matters
Using DAX Studio to identify and optimize slow measures was essential for production readiness—users won't adopt tools that take minutes to load.

---

## 📝 Data Privacy Notice

All agent names, financial figures, and operational data presented in this repository have been fully anonymized and modified to protect client confidentiality. The dashboard architecture, methodology, DAX logic, data models, and analytical approaches accurately reflect the production solutions delivered.

---

## 🔗 Connect

**LinkedIn:** [linkedin.com/in/jebarrioscornett](https://linkedin.com/in/jebarrioscornett)

**Individual Project Details:**
- [Billing Project Full Documentation](./Billing-Project/README.md)
- [Productivity Project Full Documentation](./Productivity-Project/README.md)

---

*Portfolio Last Updated: March 2026*
