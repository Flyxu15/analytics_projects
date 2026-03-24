# DAX Measures — Fly Analytics Billing Dashboard

> Complete measure library for the Agent Billing & Compliance Dashboard, with business context, technical explanation, and implementation notes.

---

## Overview

The billing dashboard relies on a set of DAX measures that translate raw transaction and salary data into actionable compliance metrics. The measures are organized across three areas: **core billing KPIs**, **salary vs. output comparisons**, and **dynamic period filtering** for month-over-month analysis.

| Category | Measures | Complexity |
|----------|----------|------------|
| Core Billing KPIs | 3 | Basic–Medium |
| Salary vs. Output | 3 | Medium |
| Dynamic Period Filtering | 2 | Advanced |
| Agent Detail Metrics | 2 | Medium |

**Total Measures in Dashboard:** 15+  
**Showcased Here:** Most impactful ones with full context

---

## Core Billing KPIs

### Total Salary
**Business Purpose:** Baseline salary figure used across all compliance and delta calculations

```dax
Salario = 4535691
```

> **Note:** In the production version this is dynamically calculated per agent and period. This simplified version is used in portfolio demonstrations with anonymized data.

---

### Total Transaction Cost
**Business Purpose:** Sum of all billable unit costs processed by an agent in a given period — the core output metric

```dax
Total Costo Unitario = SUM('ALL BD'[Costo Unitario])
```

**Key Features:**
- Responds to all filter contexts (agent, period, team, classification)
- Used as the numerator in compliance rate calculations
- Compared directly against salary to derive the efficiency delta

---

### Average Compliance Rate
**Business Purpose:** Primary KPI — measures what percentage of salary is covered by transaction output

```dax
Avg Compliance = 
DIVIDE(
    [Total Costo Unitario],
    [Salario]
)
```

**Key Features:**
- Safe division with `DIVIDE` — returns blank instead of error on zero denominator
- Drives all conditional formatting across the dashboard (color-coded agent rows)
- Period-over-period trend tracked via sparkline and % change indicator

**Business Interpretation:**
- `>70%` → High performer (blue highlight)
- `50–70%` → On track
- `<50%` → Underperforming — flagged for management review

---

## Salary vs. Output Comparisons

### Cost Difference (Simple)
**Business Purpose:** Quick delta between salary and transaction output per agent

```dax
Diferencia1 = [Salario] - [Total Costo Unitario]
```

**Business Interpretation:**
- Positive value → Agent cost exceeds output (productivity gap)
- Near zero → Agent is cost-neutral
- Used in the Agent Summary table as "Total Difference" column

---

### Cost Difference (Context-Aware)
**Business Purpose:** More robust version using SUMX to correctly handle row-level filter context in matrix visuals

```dax
Diferenci1a = 
SUMX(
    VALUES('Dashboard resumen indicador'),
    [Salario] - [Costo transacciones]
)
```

**Why SUMX here:**
- Matrix visuals iterate over rows — SUMX ensures the subtraction happens at the correct granularity (per agent, per period)
- Prevents incorrect aggregation when multiple agents are visible simultaneously
- `VALUES()` respects the current filter context without removing it

**When to use this vs. the simple version:**
- Simple version: Single-agent views, card visuals
- SUMX version: Matrix tables, multi-agent comparisons

---

### Total Points Achieved (Target Tracking)
**Business Purpose:** Measures total monthly productivity points earned by each agent against their goal

```dax
Total Monthly Points = SUM('Targets'[Monthly Points Achieved])
```

**Used In:** Target Dashboard — both Team 1 and Team 2 views  
**Paired With:** Agent goal column to calculate point deficit/surplus per agent

---

## Dynamic Period Filtering

These measures power the month-over-month comparison feature, allowing management to select any two months and instantly compare billing output across agents or process types.

### Month 1 Process Filter
**Business Purpose:** Count records matching the first user-selected month for period comparisons

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

**Technical Breakdown:**
- `FORMAT(..., "YYYY-MM")` — converts dates to string for reliable month matching
- `SELECTEDVALUE(MesesDisponibles[Mes])` — reads the user's slicer selection dynamically
- `FILTER` — applies row-level date matching rather than modifying filter context
- `CALCULATE` — wraps the filter for proper context evaluation

---

### Month 2 Process Filter
**Business Purpose:** Count records for the second selected month — paired with Month 1 for side-by-side comparison

```dax
Procesos_Mes2 = 
CALCULATE(
    COUNTROWS('MESES'),
    FILTER(
        'MESES',
        FORMAT('MESES'[FECHA REGISTRO DEL PROCESO], "YYYY-MM") = 
        SELECTEDVALUE(MesesDisponibles1[Mes])
    )
)
```

> **Note:** `MesesDisponibles` and `MesesDisponibles1` are two separate disconnected tables, each connected to their own slicer. This pattern allows truly independent month selection without cross-filtering interference.

**Why This Pattern Is Important:**
Using `SELECTEDVALUE` with disconnected tables is a robust alternative to `DATEADD` or `SAMEPERIODLASTYEAR` when users need to compare arbitrary, non-consecutive months — a common real-world requirement in billing operations.

---

## Agent Detail Measures

### Unit Cost by Classification
**Business Purpose:** Break down an agent's total transaction cost by Agile vs. Non-Agile process classification

```dax
Total Unit Cost = SUM('ALL BD'[Costo Unitario])
```

**Used In:** Agent Detail Dashboard — grouped by Classification (Agile / Non-Agile) and Process Type  
**Business Value:** Reveals which process types are the most and least cost-efficient per agent

---

### On-Site Unit Points
**Business Purpose:** Count productivity points earned through on-site (physical branch) transactions

```dax
Total On-Site Unit Points = SUM('ALL BD'[Puntos Unitarios Presencial])
```

**Paired With:** Virtual points measure for channel split analysis  
**Business Value:** Identifies whether agents are more productive on-site or virtually — informs channel staffing decisions

---

## DAX Best Practices Demonstrated

### 1. Safe Division
Always use `DIVIDE` instead of the `/` operator to prevent divide-by-zero errors in compliance calculations:

```dax
-- ✅ Correct
DIVIDE([Total Costo Unitario], [Salario])

-- ❌ Avoid
[Total Costo Unitario] / [Salario]
```

---

### 2. SUMX for Row-Level Accuracy in Matrix Visuals
When subtracting measures inside a matrix, use `SUMX` + `VALUES()` to ensure calculations happen at the correct row granularity:

```dax
-- ✅ Correct for matrix visuals
SUMX(VALUES('Table'), [Measure A] - [Measure B])

-- ❌ Can produce wrong totals
[Measure A] - [Measure B]
```

---

### 3. Disconnected Tables for Independent Period Selection
Use separate disconnected tables (one per slicer) when users need to compare two arbitrary months:

```dax
-- Month 1 reads from MesesDisponibles
SELECTEDVALUE(MesesDisponibles[Mes])

-- Month 2 reads from MesesDisponibles1 (independent)
SELECTEDVALUE(MesesDisponibles1[Mes])
```

**Why:** Standard time intelligence functions like `DATEADD` assume consecutive periods. Disconnected tables give users full flexibility.

---

### 4. FORMAT for String-Based Date Matching
When filtering by month across datasets with different date granularities, convert to `"YYYY-MM"` string format for reliable matching:

```dax
FORMAT('Table'[Date Column], "YYYY-MM") = SELECTEDVALUE(MonthTable[Mes])
```

**Why:** Avoids mismatches between date/datetime columns and handles varying day values within the same month.

---

### 5. Measure Chaining for Maintainability
Build complex measures from simpler base measures — changes propagate automatically:

```dax
-- Base measures
[Salario] = 4535691
[Total Costo Unitario] = SUM('ALL BD'[Costo Unitario])

-- Derived measures reference the base
[Diferencia1] = [Salario] - [Total Costo Unitario]
[Avg Compliance] = DIVIDE([Total Costo Unitario], [Salario])
```

---

## Performance Optimization Notes

### DAX Studio Analysis
Performance optimization was conducted using DAX Studio during development:

- Identified measures triggering full table scans in the billing records table
- Replaced runtime date calculations with pre-formatted string columns where beneficial
- Validated that `SUMX` + `VALUES()` pattern did not introduce performance bottlenecks in the agent matrix
- Confirmed `DIVIDE` outperforms conditional `IF(denominator=0, BLANK(), ...)` pattern for compliance measures

### Key Optimizations Applied
1. **Pre-calculated classification flags** in Power Query rather than runtime DAX `IF` statements
2. **DIVIDE** for all compliance measures — avoids error handling overhead
3. **Disconnected tables** kept small (months only) to minimize cross-filter cost
4. **Measure chaining** prevents duplicate calculation logic across visuals

---

## Skills Demonstrated

✅ **Safe Division Handling** — DIVIDE across all compliance KPIs  
✅ **Row Context Awareness** — SUMX + VALUES for accurate matrix calculations  
✅ **Dynamic Period Filtering** — Disconnected table pattern for arbitrary month comparison  
✅ **Date Manipulation** — FORMAT for string-based month matching  
✅ **Measure Chaining** — Base measures reused across derived calculations  
✅ **Performance Optimization** — DAX Studio analysis and targeted query improvements  
✅ **Business Logic Translation** — Raw billing data converted to actionable compliance KPIs  

---

*For full project context and dashboard screenshots, see [README.md](README.md)*  
*For detailed case study, see [Documentation/Case-Study.pdf](Documentation/Case-Study.pdf)*
