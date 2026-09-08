**Lab Experiment 5: Time Series Analysis for Sales Data using Power BI**

**Aim**

To perform time series analysis on sales data using Power BI by analyzing monthly sales trends, month-to-month changes, sales growth, moving averages, and year-over-year performance.

**Procedure**

**1. Import and Prepare the Data**
Import the following datasets into Power BI:

    Customers
    Orders
    Order Items
    Products

Open:  Home → Transform Data

Using Power Query:

  Remove unnecessary columns
  Rename relevant columns
  Change appropriate data types
  Filter data where required
  Replace values where required
  Ensure Order Date is set to Date

Click:  Close & Apply

**2. Create Relationships**

Go to Model View and create the required relationships between the tables using:

    Customer ID
    Order ID
    Product ID

Ensure that Order Date from the Orders table is available for time-based analysis.

**3. Create a Calendar Table**

Go to: Modeling → New Table
Calendar = CALENDAR(MIN(Orders[order_date]),MAX(Orders[order_date]))

Create the required columns:
Year = YEAR(Calendar[Date])

Month = FORMAT(Calendar[Date], "MMM")

Month Number = MONTH(Calendar[Date])

Sort Month by Month Number.

Create the relationship: Calendar[Date] → Orders[order_date]

**4. Create the Required DAX Measures**

**Total Sale**s
Total Sales = SUMX('Order Items','Order Items'[quantity] *RELATED(Products[unit_price]) *(1 - 'Order Items'[discount_rate]))

**Previous Month Sales**
Previous Month Sales = CALCULATE([Total Sales],DATEADD(Calendar[Date],-1,MONTH))

**Sales Change**
Sales Change = [Total Sales] - [Previous Month Sales]

**Sales Growth %**
Sales Growth % = DIVIDE([Sales Change],[Previous Month Sales])

Format Sales Growth % as Percentage.

**3-Month Moving Average**
3 Month Moving Average = AVERAGEX(DATESINPERIOD(Calendar[Date],MAX(Calendar[Date]),-3,MONTH),[Total Sales])

**Previous Year Sales**
Previous Year Sales = CALCULATE([Total Sales],SAMEPERIODLASTYEAR(Calendar[Date]))

**YoY Sales Growth %**
YoY Sales Growth % = DIVIDE([Total Sales] - [Previous Year Sales],[Previous Year Sales])


**5. Monthly Sales Trend**
Create a Line Chart.

  Calendar[Month] → X-axis
  [Total Sales] → Y-axis

Title:  Monthly Sales Trend

Identify:
  Highest sales month
  Lowest sales month

**6. Month-to-Month Sales Analysis**
Create a visual using:

Calendar[Month] → X-axis
[Sales Change] → Y-axis

Title: Month-to-Month Sales Change

Create another visual using:

Calendar[Month] → X-axis
[Sales Growth %] → Y-axis

Title: Monthly Sales Growth %

Identify periods of sales increase and decrease.

**7. Moving Average Analysis**
Create a Line Chart containing:

Calendar[Month] → X-axis
[Total Sales] → Y-axis
[3 Month Moving Average] → Y-axis

Title: Actual Sales vs 3-Month Moving Average

Interpret whether the overall sales trend is increasing, decreasing, or fluctuating.

**8. Year-over-Year Analysis**
If the dataset contains multiple years, create a suitable visual comparing:

[Total Sales]
[Previous Year Sales]

Use Calendar[Month] or Calendar[Year] as the time dimension.

Also analyze:

[YoY Sales Growth %]

Title: Year-over-Year Sales Comparison

If the dataset contains only one year, this step may be omitted or replaced with another suitable time-period comparison.

**9. Add Date Slicer**
Add a Slicer using:

Calendar[Date]

Allow the user to select a specific date range and observe how the time-series analysis changes.

**10. Create the Time Series Report**
Create a single report page containing:

**Summary**
    Total Sales Card
**Analysis**
    Monthly Sales Trend
    Month-to-Month Sales Change
    Monthly Sales Growth %
    Actual Sales vs 3-Month Moving Average
    Year-over-Year Sales Comparison, where applicable

**Interactivity**
    Date Slicer

Finally, identify at least three meaningful business insights from the analysis.

**Expected Output**

<img width="601" height="333" alt="eda5" src="https://github.com/user-attachments/assets/a4a60ed3-4aa1-47d7-9c04-291f8877f5be" />


**Result**
Thus, the sales data was successfully analyzed using time-series techniques in Power BI. Monthly trends, sales changes, growth rates, moving averages, and year-over-year performance were calculated and visualized to create an interactive Time Series Sales Analysis Report.
