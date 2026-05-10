# Project 2 – DAX & Data Modeling

## Overview
This lab activity focuses on using DAX (Data Analysis Expressions) in Power BI for data aggregation, filtering, and table creation. It also covers basic data modeling concepts such as star schema and relationships between tables.

---

## DAX Concepts

### Single Scalar Output
Returns a single value as output.

Example:
```sql
SELECT MAX(salary) FROM employee;
```

### Table Output
Returns a complete table as output.

Example:
```sql
SELECT dname, MAX(sal)
FROM emp
GROUP BY dname;
```

---

## Activity 10 – Working with Group By DAX

### Region-wise Sales
Created a new table to display total sales region-wise using SUMMARIZE.

```DAX
Region Wise Sales =
SUMMARIZE(
    Orders,
    Orders[Region],
    "Total Sales", SUM(Orders[Sales])
)
```

### Sub-Category Wise Sales & Profit
Generated sales and profit report category-wise.

```DAX
Sub Cat Wise Report =
SUMMARIZE(
    Orders,
    Orders[Sub-Category],
    "Total Sales", SUM(Orders[Sales]),
    "Total Profit", SUM(Orders[Profit])
)
```

---

## Working with Filters

Filtered data using conditions:
- Consumer segment
- Central and South regions
- First Class ship mode
- Quantity greater than 10

```DAX
Result =
CALCULATETABLE(
    Orders,
    Orders[Segment] = "Consumer",
    Orders[Region] IN {"Central", "South"},
    Orders[Ship Mode] = "First Class",
    Orders[Quantity] > 10
)
```

### Display Customer Names

```DAX
Cust =
SELECTCOLUMNS(
    CALCULATETABLE(
        Orders,
        Orders[Segment] = "Consumer",
        Orders[Region] IN {"Central", "South"},
        Orders[Ship Mode] = "First Class",
        Orders[Quantity] > 10
    ),
    "cust name",
    Orders[Customer Name]
)
```

---

## Activity 11 – Data Modeling

### Star Schema
Star schema is a data modeling technique where:
- A central Fact Table stores measurable data
- Dimension Tables contain descriptive information
- Relationships connect fact and dimension tables

This model improves data analysis and reporting efficiency in Power BI.

---

## Tools Used
- Power BI Desktop
- DAX
- SQL
- Data Modeling
