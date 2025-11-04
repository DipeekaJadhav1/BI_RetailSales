<img width="627" height="607" alt="image" src="https://github.com/user-attachments/assets/c52d5719-dec5-45f4-ad79-90f3247578d5" />


## Data Model Setup


•	Sales → Products via ProductID

•	 Sales → Customers via CustomerID

•	Sales → Dates via OrderDate = Date


Data Cleaning 

Using Power Query Editor:

 • Replaced blank Regions with “Unknown”. 
 
• Removed duplicate rows from Customers table.

 • Added calculated column:
 
SalesAmount = [Quantity] * [UnitPrice] * (1 - [Discount]) 


Dashboard Layout


• KPI Cards: 

Total Sales, Total Profit, Average Discount. 

• Sales by Region: Bar chart showing regional performance.

 • Sales by Category: Pie chart showing category-wise sales share.
 
 • Monthly Sales Trend: Line chart showing sales over time. 
 

DAX Measure – Profit

	Total Sales = SUM(Sales[SalesAmount]) 
  
Total Cost = SUMX(Sales, Sales[Quantity] * RELATED(Products[CostPrice]))

 Profit = [Total Sales] – [Total Cost]
 
DAX Measure – YTD Sales

	YTD Sales = TOTALYTD(SUM(Sales[SalesAmount]), 'Dates'[Date])
  
 Explanation: Calculates cumulative sales from the start of the year to each date.
 
 	Visual: Line chart showing Monthly Year-to-Date Sales Trend. 
  


DAX Measure – Top 5 Products

Created a Bar Chart with Products[ProductName] on Axis and SalesAmount on Values. Applied Top N filter to display Top 5 Products by SalesAmount and sorted descending. This highlights the best-performing products by revenue.

DAX Measure – Profit Margin % 

Profit Margin % = DIVIDE([Profit], [Total Sales], 0)

 Displayed as a KPI Card, formatted as percentage. 
 
Shows the portion of sales converted to profit for quick performance insight


Slicer Interaction 

Added interactive Slicers for Region, Category, and Month: 

• Region → Customers[Region] 

• Category → Products[Category] 
• Month → Dates[Month] All visuals update dynamically when filters are applied, enhancing user interaction.

