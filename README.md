# 📊 Restaurant Sales & Performance Analytics Dashboard
A comprehensive **Power BI dashboard** for a multi-location restaurant chain, analyzing sales performance, customer satisfaction, and operational efficiency across 12 locations with 8,546+ transactions.

### 🎯 Business Impact
- **$25,799+** in analyzed sales
- **12 locations** across US
- **4.2/5** average customer rating
- **3 key order types**: Dine-In, Delivery, Takeaway

---

## 📊 Dashboard Features

### 1. Executive Dashboard
- Real-time KPI cards (Total Revenue, Orders, Rating, Items)
- Performance by Location
- Sales by Menu Category
- Sales by Order Type
- Sales Trend (YTD)
- Correlation between Ratings and Sales

### 2. Sales Analysis
- Sales Breakdown
- **Heat Map**: Day/Hour performance
- Location-based performance
- Product portfolio analysis

### 3. Customer Analytics
- Rating distribution analysis
- NPS score calculation
- Correlation between ratings and sales
- Delivery vs. Dine-In comparison

### 4. Performance Product
- Pareto analysis (80/20 rule)
- Summary Products Table
- Menu optimization recommendations

---

### 🏆 Key Insights Delivered

1. **Sales Optimization**
   - Top performing location: **Coral Gables** (18% of total sales)
   - Best-selling category: **Main Dishes** (65% of revenue)
   - Highest revenue item: **NY Strip Steak** ($3,496.94)

2. **Customer Experience**
   - Highest rated category: **Beverage** (4.31 avg rating)
   - Delivery orders have **12% lower ratings** than dine-in
   - **Friday evenings** show 35% higher sales

3. **Operational Efficiency**
   - Peak hours: **12-1 PM** and **6-8 PM**
   - Lowest activity: **Sunday mornings**
   - **$142** average order value
  
4. ## 📋 Product Portfolio Optimization

| Category | Sales % | Avg Rating | Recommendation |
| :--- | :---: | :---: | :--- |
| **Main** | 65% | 3.89 | ✅ Maintain & promote |
| **Beverage** | 18% | 4.07 | ✅ Expand selection |
| **Appetizer** | 10% | 3.98 | ✅ Bundle with mains |
| **Dessert** | 7% | 3.87 | ⚠️ Improve offerings |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Power BI** | Dashboard creation & visualization |
| **Power Query** | Data transformation & cleaning |
| **DAX** | Advanced calculations & measures |
| **Excel** | Initial data storage |
| **Git** | Version control |

---

## 🎨 Theme & Design
The dashboard follows a professional **green corporate theme** aligned with the restaurant industry:
- 🌿 **Primary**: Forest Green (#1B5E20)
- 🌱 **Secondary**: Medium Green (#2E7D32)
- 🍃 **Accent**: Light Green (#66BB6A)
- ⚪ **Background**: Off-white (#F5F7F5)

---

## 📈 Key DAX Measures
Calendar = 
VAR MinDate = MIN('Restaurant Sales'[Order Date])
VAR MaxDate = MAX('Restaurant Sales'[Order Date])
RETURN
ADDCOLUMNS(
    CALENDAR(MinDate, MaxDate),
    "YEAR", YEAR([Date]),
    "MONTH", FORMAT([Date],"MMM"),
    "NUMBERMONTH", MONTH([Date]),
    "QUARTER","Q" & QUARTER([Date]),
    "WEEKDAY", FORMAT([Date],"ddd"),
    "DAYNUMBER", WEEKDAY([Date]),
    "WEEKYEAR", WEEKNUM([Date])
)

Locations = 
DISTINCT('Restaurant Sales'[Restaurant Location])

Average Price Order = 
AVERAGEX('Restaurant Sales',[Order Total])

Average Ratings = 
AVERAGE('Restaurant Sales'[Customer Rating])

Avg Price Item = 
DIVIDE([Total Sales],[Total Items])

Best Category Rating = 
    MAXX(
        VALUES('Restaurant Sales'[Category]),
    [Average Ratings]
    )

Category Participation = 
    DIVIDE(
        [Total Sales],
        CALCULATE([Total Sales],
        ALLSELECTED('Restaurant Sales'[Category]))
    )

Total Sales = 
SUM('Restaurant Sales'[Order Total])

Total Orders = 
COUNTROWS('Restaurant Sales')

Sales YTD = 
TOTALYTD([Total Sales], 'Calendar'[Date])

Sales MM AA = 
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Calendar'[Date])
)


