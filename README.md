# SQL, PowerBI Interactive Dashboard for Sample Store Data Analysis

## Overview

This repository presents an intricately crafted interactive dashboard developed with PowerBI to represent the Sample Store data. SQL scripts are used for preprocessing, querying, and generating insights from the dataset before visualizing it in PowerBI. The project rigorously analyzes trends and patterns within the dataset, leveraging SQL for robust data manipulation and PowerBI's advanced features for interactive charting and graphing. The primary goal is to augment data comprehension and enable the seamless communication of insights.

The resultant comprehensive dashboard offers a visually engaging representation of key findings, empowering users to extract meaningful conclusions from the Sample Store data.





![ss](Super_store_db_ss.png)



## Dataset

- The dataset contains 21 variables, including Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, Country, City, State, Postal Code, Region, Product ID, Category, Sub-Category, Product Name, Sales, Quantity, Discount, and Profit.
- The dataset spans from 2014 to 2017, encompassing sales details across all U.S. states.
- All monetary values are in US($) currency.
- Three distinct customer segments: Home Office, Consumer, and Corporate.
- Products are categorized into Furniture, Office Supplies, and Technology.
- Four regional classifications for U.S. states: Central, South, East, and West.
- There are 17 items accounting for sub-categories.

##SQL Integration 

SQL scripts are provided to handle the following operations:

1. Data Preprocessing
Removing duplicate entries:
```sql
    DELETE FROM sample_store_data  
    WHERE RowID IN (SELECT RowID FROM sample_store_data GROUP BY RowID HAVING COUNT(*) > 1);
```

Handling missing or null values
```sql
   UPDATE sample_store_data  
   SET Profit = 0  
   WHERE Profit IS NULL; 
```

2. Querying Data
Calculating total sales, quantity, and profit:
```sql
   SELECT  
     SUM(Sales) AS Total_Sales,  
     SUM(Quantity) AS Total_Quantity,  
     SUM(Profit) AS Total_Profit  
   FROM sample_store_data; 
```
Analyzing profit trends by category and year:
```sql
   SELECT  
     Category,  
     YEAR(OrderDate) AS Year,  
     SUM(Profit) AS Total_Profit  
   FROM sample_store_data  
   GROUP BY Category, YEAR(OrderDate)  
   ORDER BY Total_Profit DESC; 
```
Identifying top-performing sub-categories:
```sql
   SELECT  
     Sub_Category,  
     SUM(Profit) AS Sub_Category_Profit  
   FROM sample_store_data  
   GROUP BY Sub_Category  
   ORDER BY Sub_Category_Profit DESC; 
```

3. Data Export
The queried results are exported to CSV files using SQL or ETL tools for seamless integration with PowerBI.

## Dashboard

Information obtained from the dashboard:

- All visualizations are customized, allowing analysis based on U.S. states.
- Sum of Sales, Sum of Quantity, Sum of Profit.
- Profit breakdown by Category, Segment, and Region.
- Sub-Category profit analyzed across the years from 2014 to 2017.
- Profit by Sub-Category based on the sum of profit.
- Table illustrating total sales by sub-category and region.

 ## Results from SQL and Dashboard Analysis:

 SQL Results:

 - Total sales amount is $2.30M, with 38K units sold, and total profit is $286.40K.
 - Highest sub-category profits observed from 2016 to 2017, peaking around October to November.
 - Copiers emerge as the most profitable sub-category.

 Dashboard Highlights:

 - Technology leads with 50.76% of the total profit, followed by Consumer.
 - Consumer segment dominates with 46.83% of the total profit.
 - Western region states exhibit the highest profit, followed by Eastern, Southern, and Central regions.

## Conclusion

The PowerBI dashboard, enhanced with SQL preprocessing and querying offers a comprehensive analysis of sales data, providing valuable insights for strategic decision-making. The dataset, spanning 2014 to 2017, encompasses diverse U.S. states, allowing for tailored visualizations based on geographic regions. Key highlights include peak sub-category profits observed in the latter years, with Copiers emerging as a standout category. Technology products significantly contribute to the overall profit share, particularly in the Western region. The dominance of Consumer segment profits and regional variations underscores the importance of targeted strategies. The interactive and customizable nature of the dashboard powered by SQL-backed data analytics enhances its utility for extracting actionable business intelligence.
