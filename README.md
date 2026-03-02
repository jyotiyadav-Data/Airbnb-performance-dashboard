# Airbnb-performance-dashboard

# 🌍 Global Airbnb Performance Dashboard | Power BI

## 📌 Project Overview

The **Global Airbnb Performance Dashboard** is an end-to-end data analytics project built using Power BI.  
This dashboard analyzes Airbnb listings across major global cities and provides business insights into listing growth, pricing strategy, city performance, and customer ratings.

The project demonstrates strong DAX fundamentals, ranking logic, cumulative percentage (Pareto) analysis, and business storytelling through interactive visualizations.

---

## 🎯 Business Objective

- Analyze listing distribution across cities  
- Identify top-performing cities  
- Understand room-type pricing strategy  
- Compare Superhost vs Non-Superhost performance  
- Study growth trends and COVID-19 impact  
- Evaluate city-wise rating performance  

---

## 🛠 Tools & Technologies

- Power BI  
- DAX (Data Analysis Expressions)  
- Data Modeling  
- Interactive Dashboard Design  

---

## 📊 Key KPIs

- **279,712** Total Listings  
- **5,373K** Total Reviews  
- **182,024** Hosts  
- **144** Property Types  
- **10** Major Cities Analyzed  

---

## 📈 Dashboard Insights

### 1️⃣ Listing Growth Trend
- Rapid growth until 2015 (Peak year)
- Regulatory slowdown in 2016–2017
- Significant decline during COVID-19 period
- Room-type contribution breakdown

### 2️⃣ Market Share by City (Pareto Analysis)
- Paris, NYC, and Sydney contribute nearly 50% of total listings
- City ranking based on total listings
- Cumulative percentage logic applied using DAX

### 3️⃣ Average Price by Room Type
- Hotel Rooms have the highest average price
- Entire Place is the most preferred premium option
- Private and Shared rooms are budget segments

### 4️⃣ Ratings Analysis
- Mexico City and Rio are among the highest-rated cities
- Detailed review score analysis:
  - Accuracy
  - Cleanliness
  - Communication
  - Location
  - Value for Money

### 5️⃣ Superhost Impact
- Superhosts significantly contribute to listing quality
- Comparison between Superhost and Non-Superhost listings

---

# 📐 DAX Measures Used

## Rating Measures

```DAX
Accuracy = AVERAGE(Listings[review_scores_accuracy])

Avg Rating = AVERAGE(Listings[review_scores_rating])

Cleanlines = AVERAGE(Listings[review_scores_cleanliness])

Communication = AVERAGE(Listings[review_scores_communication])

Location = AVERAGE(Listings[review_scores_location])

Value for money = AVERAGE(Listings[review_scores_value])
```

---

## Price Measure

```DAX
AVG Price = AVERAGE(Listings[price])
```

---

## Room Type Measures

```DAX
Entire Place = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Entire place"
)

Hotel Room = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Hotel room"
)

Private Room = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Private room"
)

Shared Room = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Shared room"
)
```

---

## Superhost Measures

```DAX
Superhost Listing = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[host_is_superhost] = "t"
)

No Superhost Listing = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[host_is_superhost] = "f"
)
```

---

## Ranking & Pareto Logic

### City Rank

```DAX
City Rank = 
RANKX(
    ALL(Listings[city]),
    [Total listing],
    ,
    DESC
)
```

### Cumulative Listing

```DAX
Cumulative Listing = 
VAR CurrentRank = 
MAXX(
    VALUES(Listings[city]),
    [City Rank]
)
RETURN
CALCULATE(
    [Total listing],
    FILTER(
        ALL(Listings[city]),
        [City Rank] <= CurrentRank
    )
)
```

### Cumulative %

```DAX
Cumulative % = 
DIVIDE(
    [Cumulative Listing],
    CALCULATE([Total Listings], ALL(Listings[city]))
)
```

---

## 💡 What This Project Demonstrates

- Advanced DAX usage (RANKX, CALCULATE, FILTER, DIVIDE)
- Cumulative percentage & Pareto analysis
- KPI-based dashboard design
- Business-oriented data storytelling
- Real-world analytics problem solving

---

## 🚀 Conclusion

This project showcases the ability to:

- Transform raw data into business insights  
- Apply advanced DAX logic  
- Design professional dashboards  
- Communicate insights clearly  

---

⭐ If you found this project useful, consider giving it a star!
