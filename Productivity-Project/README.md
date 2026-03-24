# Customer Service Analytics Dashboard | Power BI

> **Production Power BI analytics solution delivered as IT Analyst - comprehensive platform for tracking agent productivity and service quality in energy company operations**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

---

## 📊 Business Problem

**Challenge:** Energy company customer service operations had no centralized system to measure and track agent productivity. Managers lacked visibility into:
- Individual agent performance against SLA targets
- Productivity patterns across time periods and service groups  
- Regional and branch performance comparisons
- Process completion times and bottlenecks
- Customer satisfaction metrics

**Impact:** Inefficient resource allocation, inconsistent service quality, and limited ability to identify top performers or coach underperformers.

---

## 💡 Solution Overview

Developed and deployed a **13-page Power BI analytics platform** as an IT Analyst that consolidates ticketing, agent performance, service channels, and process management data into a unified real-time monitoring system. Currently used daily by management for operational decision-making and resource planning.

### Key Features
- **Real-time SLA Tracking:** Monitor service level compliance across 28,000+ tickets
- **Agent Performance Analysis:** Individual and comparative metrics for 60+ customer service agents
- **Peak Hours Optimization:** Identify high-volume periods for data-driven staffing decisions
- **Process Management:** Track 75,000+ processes across claims, complaints, petitions, and orders
- **Customer Satisfaction:** Analyze 187,000+ survey responses with 99.1% approval rate
- **Regional Comparisons:** Performance benchmarking across 4 regions and 10+ branches

---

## 📈 Key Metrics & Dimensions

### Business Metrics
| Metric | Description | Target |
|--------|-------------|--------|
| **Wait Service Level** | % of tickets with <15 min wait time | >60% |
| **Service Time** | Avg time to resolve ticket | <7 min |
| **Abandonment Rate** | % of tickets abandoned | <5% |
| **Daily Ticket Volume** | Avg tickets per day | ~700 |
| **Customer Satisfaction** | Survey approval rate | >95% |

### Dimensions
- **Time:** Hourly, daily, weekly, monthly, year-over-year
- **Geography:** 4 regions (Central, East, North, South), 10+ branches
- **Service Types:** Damages, Claims, Financing, Notifications, General Assistance
- **Process Categories:** Claims (20.4%), Complaints (20.1%), Suggestions (20%), Petitions (19.9%), Orders (19.7%)
- **Agents:** 60+ customer service representatives with individual KPIs

---

## 🔍 Key Insights & Findings

### 1. Service Level Performance Gap
**Finding:** Overall wait service level of 36.82% (under 15 minutes) falls significantly below target  
**Impact:** Only 1,571 of 4,267 tickets met the wait time target  
**Root Cause:** Queue management bottleneck, not agent efficiency (82.63% meet service time targets)

### 2. Peak Hour Patterns
**Finding:** Highest volume at 9:00 AM (425 tickets) with 38.12% service level  
**Insight:** Morning hours perform better despite higher volume  
**Implication:** Afternoon staffing levels or fatigue may be reducing efficiency

### 3. Regional Consistency 
**Finding:** All regions perform within narrow 35.83% - 36.97% range  
**Insight:** Indicates systemic process issues rather than regional management problems  
**Action:** Focus on organization-wide improvements vs. region-specific fixes

### 4. Agent Performance Variance
**Finding:** 22+ percentage point gap between top (57.14%) and bottom (34.41%) performers  
**Opportunity:** Significant coaching and standardization potential  
**Value:** Bringing all agents to top-quartile performance could improve overall SLA by 15-20%

### 5. Process Type Concentration
**Finding:** Basic Data Change (8.4K) and General Information (6.7K) represent 20% of all processes  
**Opportunity:** High-volume, routine processes are prime automation candidates  
**Potential Impact:** Automating top 2 process types could reduce agent workload by 20%

### 6. Seasonal Volume Trends
**Finding:** 12.1% volume increase from December (20,188) to January (22,622)  
**Pattern:** Consistent month-over-month growth in specific categories  
**Value:** Enable proactive resource planning for predictable spikes

---

## 💼 Business Recommendations

### Immediate Actions (0-30 Days)

**1. Queue Management Optimization**  
**Problem:** 82.63% meet service time targets but only 36.82% meet wait time targets  
**Recommendation:** Implement skills-based routing and real-time queue monitoring  
**Expected Impact:** 10-15% improvement in wait service level within first month

**2. Afternoon Staffing Adjustment**  
**Problem:** Performance drops significantly after 2:00 PM (33.53% at 4:00 PM)  
**Recommendation:** Add 2-3 agents during 2:00-5:00 PM shift, reduce morning staff by 1-2  
**Expected Impact:** Better load distribution, 5-7% SLA improvement in afternoon

**3. Top Performer Recognition & Best Practice Sharing**  
**Problem:** 22-point performance gap between agents  
**Recommendation:** Document and share techniques from top 10% performers (e.g., Angela Penn at 57.14%)  
**Expected Impact:** Raise bottom 25% by 8-10 percentage points through peer learning

### Short-Term Initiatives (1-3 Months)

**4. Process Automation Strategy**  
**Problem:** Basic Data Change (8.4K) and General Information (6.7K) consume 20% of agent capacity  
**Recommendation:** Develop self-service portal for top 5 routine processes  
**Expected Impact:** Free up 10-12 agent hours per day for complex customer issues

**5. Regional Best Practice Exchange**  
**Problem:** All regions underperform similarly (35-37% range)  
**Recommendation:** Cross-regional task force to identify and scale successful tactics  
**Expected Impact:** Organization-wide improvements vs. regional band-aids

**6. Targeted Agent Coaching Program**  
**Problem:** Bottom quartile performers (34-36% SLA) drag down overall metrics  
**Recommendation:** 1-on-1 coaching with specific KPI targets, weekly check-ins  
**Expected Impact:** Bring bottom 25% to median performance (40%+) within 90 days

### Long-Term Strategic Moves (3-6 Months)

**7. Predictive Staffing Model**  
**Problem:** Reactive scheduling causes over/understaffing  
**Recommendation:** Build forecasting model using historical patterns (Tuesday peaks, January growth)  
**Expected Impact:** Optimize labor costs while improving service levels

**8. Customer Satisfaction Deep Dive**  
**Problem:** 99.1% approval seems inconsistent with 36.82% wait service level  
**Recommendation:** Analyze survey timing and response bias; consider post-interaction surveys  
**Expected Impact:** More accurate satisfaction measurement, identify hidden pain points

---

## 🛠️ Technical Implementation

### Technology Stack
- **Power BI Desktop:** Dashboard design and interactivity
- **DAX (Data Analysis Expressions):** Custom measures and time intelligence calculations
- **Power Query (M Language):** ETL processes and data transformation
- **DAX Studio:** Performance optimization and query tuning

### Data Architecture

**Star Schema Model:**
```
Fact Tables:
├── Tickets (28,000+ records)
│   ├── Ticket ID, Issue Date, Wait Time, Service Time
│   ├── Abandonments, Region, Branch, Agent
│   └── Service Type, Status
│
└── Processes (75,000+ records)
    ├── Process ID, Completion Date, Request Channel
    ├── Process Type, Process Group, Agent
    └── Legal Completion Date

Dimension Tables:
├── Agents (60+ records)
│   └── Agent ID, Name, Region, Branch
│
├── Services (30+ records)
│   └── Service ID, Service Name, Service Group
│
├── Time (Date table)
│   └── Date, Year, Quarter, Month, Week, Day
│
└── Geography
    └── Region, Branch, Location
```

### Key Technical Features

**1. Custom DAX Measures**

Selected examples showcasing advanced DAX techniques:

**Wait Service Level (SLA Compliance)**
```dax
Wait Service Level = 
DIVIDE(
    CALCULATE(
        COUNTROWS('DetallePorTurnoConServicio'),
        'DetallePorTurnoConServicio'[Una espera menor a 15 minutos] = 1
    ),
    CALCULATE(COUNTROWS('DetallePorTurnoConServicio'))
)
```
*Calculates percentage of tickets meeting 15-minute wait time target*

**Dynamic Process Grouping**
```dax
Process Grouped = 
VAR CurrentProcess = SELECTEDVALUE('ANUAL'[Total Processes])
VAR ProcessCount = CALCULATE(COUNTROWS('ANUAL'))
VAR TotalCount = CALCULATE(COUNTROWS('ANUAL'), ALL('ANUAL'[Total Processes]))
VAR ProcessPercent = DIVIDE(ProcessCount, TotalCount)
RETURN
IF(ProcessPercent < 0.02, "Others", CurrentProcess)
```
*Groups low-volume processes into "Others" category dynamically (under 2%)*

**Average Wait Time Calculation**
```dax
Avg. Wait = 
AVERAGEX(
    DetallePorTurnoConServicio, 
    ((DetallePorTurnoConServicio[Queue Call Date]*1440) - 
     (DetallePorTurnoConServicio[Ticket Issue Date]*1440))
)
```
*Converts datetime difference to minutes using AVERAGEX*

**Month-Based Filtering (Time Intelligence)**
```dax
Procesos_Meses11 = 
CALCULATE(
    COUNTROWS('DetallePorTurnoConServicio'),
    FILTER(
        'DetallePorTurnoConServicio',
        FORMAT('DetallePorTurnoConServicio'[Ticket Issue Date], "YYYY-MM") = 
        SELECTEDVALUE(MesesDisponibles11[Mes])
    )
)
```
*Enables dynamic month comparison for trend analysis*

**Working Days Calculation**
```dax
Working Days = 
NETWORKDAYS(
    MIN(DetallePorTurnoConServicio[Ticket Issue Date]), 
    MAX(DetallePorTurnoConServicio[Ticket Issue Date])
)
```
*Calculates business days for accurate daily averages*

*See [DAX-Measures.md](DAX-Measures.md) for complete measure library*

**2. Performance Optimization**
- Used DAX Studio to identify slow-running measures
- Optimized calculated columns vs. measures tradeoffs
- Implemented bidirectional cross-filtering for drill-through efficiency
- Reduced page load times through query plan analysis

**3. User Experience Features**
- **Dynamic Filtering:** Cascading filters across regions, branches, agents, time periods
- **Conditional Formatting:** Color-coded performance indicators (green/yellow/red for SLA targets)
- **Drill-Through Actions:** Click summary metrics to navigate to detailed views
- **Bookmarks & Navigation:** Intuitive 13-page navigation with consistent branding

---

## 📸 Dashboard Screenshots

### Home Dashboard - Executive Overview
![Home Dashboard](screenshots/home_dashboard.png)
*Executive KPI summary with 4,267 tickets, 36.82% service level, regional performance breakdown*

### Peak Hours Analysis
![Peak Hours](screenshots/peak_hours.png)
*Time-based patterns showing Tuesday peaks (1,097 tickets) and optimal staffing windows*

### Agent Performance Tracking
![Agent Performance](screenshots/agent_performance.png)
*Individual agent metrics with 68.03% wait service level and performance rankings*

### Service Level Compliance
![Service Level](screenshots/service_level.png)
*SLA tracking across wait time and service time dimensions*

### Process Management
![Processes](screenshots/processes.png)
*75,946 processes across Claims, Complaints, Suggestions, Petitions, and Orders*

---

## 📊 Dashboard Structure (13 Pages)

| Page | Purpose | Key Metrics |
|------|---------|-------------|
| **Home** | Executive overview | Total tickets, abandonments, service level %, regional breakdown |
| **Peak Hours** | Time-based analysis | Hourly/daily patterns, optimal staffing periods |
| **Agents** | Individual performance | Agent rankings, ticket volume, SLA compliance |
| **Groups** | Service group analysis | Participation %, service time by group |
| **Groups Comparison** | Month-over-month trends | Group performance over time |
| **Services** | Service-level metrics | Top services by volume, agent performance matrix |
| **Services Comparison** | Temporal service analysis | Seasonal patterns, emerging needs |
| **Agent SLA** | SLA compliance tracking | Wait time & service time by agent |
| **Processes** | Process management | Distribution across 5 process categories |
| **Process Comparison (Groups)** | Process trends by group | Monthly volume changes |
| **Process Type** | Granular process analysis | Top process types, agent contributions |
| **Process Comparison (Type)** | Process type trends | Month-over-month forecasting |
| **Surveys** | Customer satisfaction | 187K responses, approval rate, channel distribution |

---

## 🎯 Business Impact

### Quantifiable Outcomes
- **Visibility:** Delivered organization's first centralized agent performance tracking system (previously non-existent)
- **Time Savings:** Eliminated 8+ hours of weekly manual reporting, enabling real-time access to operational metrics
- **Data-Driven Decisions:** Management now uses dashboard daily for shift scheduling based on peak hour analysis
- **Accountability:** Agents self-monitor performance in real-time, improving engagement and results
- **Proactive Planning:** Month-over-month trend monitoring enabled advance resource allocation (e.g., 12% January spike identified and staffed proactively)

### Strategic Value
- **Performance Management:** Objective evaluation framework actively used for 60+ agent reviews and coaching
- **Process Improvement:** Identified high-impact automation opportunities (Basic Data Change: 8.4K processes)
- **Resource Optimization:** Evidence-based staffing decisions reducing costs during low-volume periods
- **Executive Visibility:** Leadership uses comprehensive service delivery insights for quarterly strategic planning
- **Production Stability:** Solution deployed and running with minimal maintenance, demonstrating robust design

---

## ⏱️ Project Timeline

**Duration:** 1 Month (Requirements to Production Deployment)  
**Role:** IT Analyst  
**Delivery Model:** Agile development with stakeholder feedback loops

| Week | Focus Area | Deliverables |
|------|-----------|--------------|
| **Week 1** | Foundation | Requirements documentation, data model, relationships, stakeholder alignment |
| **Week 2** | Core Dashboards | Home, Peak Hours, Agents, Groups pages with initial KPIs |
| **Week 3** | Advanced Analytics | Process analysis, SLA tracking, comparisons, user feedback integration |
| **Week 4** | Production Deployment | DAX optimization, UAT, training, production release |

**Industry Benchmark:** Similar scope typically requires 6-8 weeks  
**Achievement:** Delivered 25-35% faster through effective planning, stakeholder communication, and technical execution  
**Post-Deployment:** Stable production performance with minimal maintenance required

---

## 🚀 Skills Demonstrated

### Technical Skills
- Power BI development and dashboard design
- DAX for complex calculations and time intelligence
- Power Query (M) for ETL and data transformation
- DAX Studio for performance optimization
- Star schema data modeling
- Data visualization best practices

### Business Skills
- Requirements gathering and stakeholder management
- Business process analysis and KPI definition
- Data storytelling and insight communication
- Problem-solving and root cause analysis

### Project Management
- Solo project delivery under tight deadlines
- Agile development methodology
- Quality assurance and testing
- Technical documentation

---

## 📁 Repository Structure

```
FlyAnalytics-PowerBI-Dashboard/
├── README.md                          # This file
├── Documentation/
│   ├── Case-Study.pdf                 # Detailed project case study
│   ├── Data-Model-Diagram.png         # Star schema visualization
│   └── Technical-Specifications.md    # Detailed tech specs
├── Screenshots/
│   ├── home_dashboard.png
│   ├── peak_hours.png
│   ├── agent_performance.png
│   ├── service_level.png
│   └── processes.png
├── DAX-Measures/
│   ├── time-intelligence.dax          # Date calculations
│   ├── service-level-metrics.dax      # SLA calculations
│   └── agent-performance.dax          # Agent KPIs
└── Power-Query/
    ├── data-transformation.m          # ETL scripts
    └── date-table-generation.m        # Calendar table logic
```

---

## 🔗 Additional Resources

- **Full Case Study (PDF):** [View detailed case study](Documentation/Case-Study.pdf)
- **Data Model Diagram:** [View star schema](Documentation/Data-Model-Diagram.png)
- **LinkedIn Profile:** [Connect with me](#)

---

## 📝 License & Usage

This project represents real work I delivered as an IT Analyst for an energy company's customer service operations. The dashboard design, DAX logic, data model architecture, and analytical approach are original work I developed and deployed to production.

**Portfolio Version:** Data has been fully anonymized and modified using a different database to protect confidential business information while preserving the analytical patterns, technical implementation, and business logic that demonstrate my Power BI expertise.

**Skills Showcased:** This anonymized version accurately represents the technical complexity, business problem-solving, and delivery capability demonstrated in the production deployment.

---

## 📧 Contact

**Portfolio Project:** Fly Analytics  
**Role:** IT Analyst  
**Interested in discussing this project or similar analytics solutions?** Feel free to reach out!

---

*Last Updated: March 2026*
