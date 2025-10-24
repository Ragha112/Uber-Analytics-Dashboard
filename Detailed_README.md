# 🚖 Uber Trip Analysis Dashboard

This project presents an **interactive Power BI dashboard** that visualizes Uber trip data to uncover meaningful insights into customer demand, trip trends, and performance KPIs across multiple dimensions such as time, payment type, and vehicle category.

---

## 📊 Project Overview

The **Uber Trip Analysis Dashboard** consolidates trip-level data to help identify:
- Peak booking times (day/night, weekdays/weekends)
- Popular routes and pickup/drop-off points
- Total booking revenue and average fare trends
- Performance by vehicle type (UberX, Uber Black, etc.)
- Customer preferences across payment modes

The goal of this dashboard is to **help decision-makers optimize pricing, resource allocation, and driver deployment** based on real data-driven insights.

---

## 📁 Data Model

The data model follows a **Star Schema** design with four core tables:

| Table | Description |
|--------|--------------|
| **Trip Details** | Fact table containing trip ID, fare, payment type, timings, and distance. |
| **Location Table** | Dimension table storing city and location details. |
| **Calendar Table** | Date dimension enabling time-based slicing. |
| **Dynamic Measure** | Custom measure table for advanced DAX calculations. |

### 🔗 Relationships
- **Trip Details → Location Table** (via `PULocationID` & `DOLocationID`)
- **Trip Details → Calendar Table** (via `Pickup Date`)
- **Dynamic Measure** stores reusable KPIs.

---

## ⚙️ Tools & Techniques

| Tool | Purpose |
|------|----------|
| **Power BI Desktop** | Main tool for visualization |
| **Power Query** | Data transformation and cleaning |
| **DAX (Data Analysis Expressions)** | Custom measures and KPIs |
| **Excel** | Initial data exploration |

---

## 🧮 Key DAX Measures
```DAX
Total Bookings = COUNTROWS('Trip Details')

Total Booking Value = SUM('Trip Details'[fare_amount])

Avg Booking Amt = DIVIDE([Total Booking Value], [Total Bookings])

Avg Trip Distance = AVERAGE('Trip Details'[trip_distance])

Avg Trip Time = AVERAGE('Trip Details'[Trip Time])

Cancellation Rate = DIVIDE(
    CALCULATE(COUNTROWS('Trip Details'), 'Trip Details'[Status] = "Cancelled"),
    [Total Bookings]
)
