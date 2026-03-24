# DAX Measures - Fly Analytics Dashboard

This document showcases key DAX measures used in the Power BI dashboard, demonstrating advanced calculation techniques and business logic implementation.

---

## Service Level Metrics

### Wait Service Level (% Under 15 Minutes)
**Business Purpose:** Track percentage of tickets meeting the 15-minute wait time SLA target

**Technical Approach:** Uses CALCULATE with conditional filtering to count compliant tickets, then DIVIDE for percentage

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

**Key Features:**
- Safe division handling (DIVIDE prevents divide-by-zero errors)
- Works with binary flag column for performance
- Responds to all filter contexts (region, branch, agent, date)

---

### Service Time Compliance (% Under 7 Minutes)
**Business Purpose:** Measure agent efficiency in resolving tickets

**Technical Approach:** Similar pattern to wait service level, tracking service time performance

```dax
Nivel de Servicio En Atencion = 
DIVIDE(
    CALCULATE(
        COUNTROWS('DetallePorTurnoConServicio'),
        'DetallePorTurnoConServicio'[Atencion menor a 7 minutos] = 1
    ),
    CALCULATE(COUNTROWS('DetallePorTurnoConServicio'))
)
```

**Usage:** Powers the service time donut chart on home dashboard

---

## Time-Based Calculations

### Average Wait Time (in Minutes)
**Business Purpose:** Calculate average customer wait time in queue

**Technical Approach:** AVERAGEX with datetime arithmetic, converting to minutes via multiplication

```dax
Avg. Wait = 
AVERAGEX(
    DetallePorTurnoConServicio, 
    ((DetallePorTurnoConServicio[Queue Call Date]*1440) - 
     (DetallePorTurnoConServicio[Ticket Issue Date]*1440))
)
```

**Key Techniques:**
- Row-by-row calculation using AVERAGEX
- Datetime to minutes conversion (multiply by 1440 minutes/day)
- Handles null values automatically

**Why This Matters:** Shows ability to work with datetime calculations, a common challenge in BI

---

### Average Service Time (in Seconds)
**Business Purpose:** Measure how long agents spend actively serving customers

**Technical Approach:** Date difference calculation converted to seconds

```dax
Avg. Service = 
AVERAGEX(
    DetallePorTurnoConServicio,
    (DetallePorTurnoConServicio[Served Date] - 
     DetallePorTurnoConServicio[Queue Call Date]) * 86400
)
```

**Key Features:**
- Converts days to seconds (multiply by 86400 seconds/day)
- AVERAGEX ensures row-level calculation accuracy
- Used in agent performance comparisons

---

### Working Days Calculation
**Business Purpose:** Calculate business days (excluding weekends) for accurate daily averages

**Technical Approach:** NETWORKDAYS function for business calendar calculations

```dax
Working Days = 
NETWORKDAYS(
    MIN(DetallePorTurnoConServicio[Ticket Issue Date]), 
    MAX(DetallePorTurnoConServicio[Ticket Issue Date])
)
```

**Business Impact:**
- Enables "Daily Avg. Tickets" to exclude weekends
- More accurate performance metrics
- Accounts for actual working days vs. calendar days

**Used In:** Daily average calculations across all dashboards

---

## Advanced DAX Patterns

### Dynamic Process Grouping
**Business Purpose:** Automatically group low-volume processes into "Others" category for cleaner visuals

**Technical Approach:** Variables + conditional logic with percentage threshold

```dax
Process Grouped = 
VAR CurrentProcess = SELECTEDVALUE('ANUAL'[Total Processes])
VAR ProcessCount = CALCULATE(COUNTROWS('ANUAL'))
VAR TotalCount = CALCULATE(COUNTROWS('ANUAL'), ALL('ANUAL'[Total Processes]))
VAR ProcessPercent = DIVIDE(ProcessCount, TotalCount)
RETURN
IF(ProcessPercent < 0.02, "Others", CurrentProcess)
```

**Why This Is Advanced:**
- **Variables:** Stores intermediate calculations for readability and performance
- **Context Manipulation:** Uses ALL() to remove filter context for total
- **Dynamic Threshold:** Automatically groups processes under 2% into "Others"
- **Business Logic:** IF statement applies classification rule

**Performance Optimization:** Variables prevent recalculating same values multiple times

---

## Time Intelligence (Month Comparisons)

### Month-Based Process Filtering
**Business Purpose:** Enable month-over-month comparison in process analysis

**Technical Approach:** FORMAT function with SELECTEDVALUE for dynamic filtering

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

**Technical Details:**
- FORMAT converts date to "YYYY-MM" string for comparison
- SELECTEDVALUE retrieves user's month selection from slicer
- FILTER creates row-level date matching
- Paired with Procesos_Meses12 for two-month comparisons

**Business Value:** Powers all "Month 1 vs Month 2" comparison charts

---

### Combined Month Total
**Business Purpose:** Sum processes across two selected months

**Technical Approach:** Simple measure reference addition

```dax
Total_Procesos = [Procesos_Meses11] + [Procesos_Meses12]
```

**Simplicity Note:** Not all measures need to be complex - this shows proper measure chaining

---

## Derived Business Metrics

### Additions (Service Delta)
**Business Purpose:** Track difference between services rendered and unique tickets

**Technical Approach:** Measure subtraction with business logic

```dax
Additions = [Total Services] - [Total Tickets]
```

**Business Interpretation:**
- Positive value: Multiple services per ticket
- Zero: One service per ticket
- Used to identify bundled service patterns

---

### Abandonment Rate
**Business Purpose:** Track customer abandonment before service

**Technical Approach:** Conditional counting with CALCULATE

```dax
Abandonments = 
CALCULATE(
    COUNTROWS('DetallePorTurnoConServicio'),
    'DetallePorTurnoConServicio'[Abandoned] = "YES"
)
```

**KPI Context:** High abandonment (>5%) indicates queue management issues

---

### Average Daily Tickets
**Business Purpose:** Normalize ticket volume by working days

**Technical Approach:** Measure division using working days calculation

```dax
Avg. Tickets = DIVIDE([Total Tickets], [Working Days])
```

**Why It Matters:** Accounts for different period lengths in comparisons

---

## Count Measures

### Total Tickets (Distinct Count)
**Business Purpose:** Count unique tickets (prevents duplicate counting)

**Technical Approach:** DISTINCTCOUNT ensures one count per ticket ID

```dax
Total Tickets = DISTINCTCOUNT(DetallePorTurnoConServicio[TicketID])
```

**vs Total Services:**
```dax
Total Services = COUNT(DetallePorTurnoConServicio[TicketID])
```

**Key Difference:** DISTINCTCOUNT vs COUNT - one ticket can have multiple service records

---

## DAX Best Practices Demonstrated

### 1. Variable Usage
✅ **Process Grouped** uses VAR for readability and performance
```dax
VAR CurrentProcess = SELECTEDVALUE(...)
VAR ProcessCount = CALCULATE(...)
RETURN IF(...)
```

**Benefits:**
- Clearer code logic
- Performance optimization (no recalculation)
- Easier debugging

---

### 2. Safe Division
✅ Always use DIVIDE instead of division operator
```dax
DIVIDE([Numerator], [Denominator])  // Handles zero gracefully
```

❌ Avoid:
```dax
[Numerator] / [Denominator]  // Errors on zero
```

---

### 3. Row Context with AVERAGEX
✅ Use X-functions for row-level calculations
```dax
AVERAGEX(Table, [Row-level expression])
```

**When to use:** Calculating averages of calculated values (not just column aggregates)

---

### 4. Filter Context Management
✅ Understand when to preserve/modify filter context
```dax
ALL('ANUAL'[Total Processes])  // Removes filter
CALCULATE(...)                  // Modifies filter
FILTER(...)                     // Row-level filter
```

---

### 5. Measure Chaining
✅ Build complex measures from simpler ones
```dax
[Additions] = [Total Services] - [Total Tickets]
[Avg. Tickets] = DIVIDE([Total Tickets], [Working Days])
```

**Benefits:** Maintainability, consistency, reusability

---

## Performance Optimization Notes

### DAX Studio Analysis Conducted
- Identified slow-running measures using query plans
- Optimized filter context in time intelligence measures
- Reduced storage engine queries through calculated column evaluation

### Key Optimizations:
1. **Pre-calculated flags** (e.g., "Una espera menor a 15 minutos") instead of runtime calculations
2. **DIVIDE function** for safe, efficient division
3. **Variable usage** in complex measures to prevent recalculation
4. **DISTINCTCOUNT** only where necessary (COUNT is faster)

---

## Measure Categories Summary

| Category | Count | Complexity Level |
|----------|-------|------------------|
| **Service Level KPIs** | 3 | Medium |
| **Time Calculations** | 3 | Advanced |
| **Time Intelligence** | 3 | Advanced |
| **Derived Metrics** | 3 | Basic-Medium |
| **Count Measures** | 2 | Basic |
| **Dynamic Grouping** | 1 | Advanced |

**Total Measures in Dashboard:** 25+  
**Showcased Here:** 7 most impressive

---

## Skills Demonstrated

✅ **Time Intelligence:** Month-over-month comparisons, date filtering  
✅ **Advanced DAX Functions:** AVERAGEX, CALCULATE, FILTER, ALL, SELECTEDVALUE  
✅ **Variables:** Performance optimization and code clarity  
✅ **Business Logic:** Conditional statements, dynamic grouping  
✅ **DateTime Calculations:** Converting between units, business day calculations  
✅ **Filter Context Management:** Understanding and manipulating evaluation context  
✅ **Performance Optimization:** Using DAX Studio to identify and fix bottlenecks  

---

*For full implementation details and dashboard usage, see [README.md](README.md)*
