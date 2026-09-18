
# Sales Data Analysis

##  Power BI Report

The Power BI report contains interactive dashboards covering sales trends, profit analysis, product performance, geographical performance, discounts, and two-period comparisons.

 [**View / Download Power BI Report (.pbix)**](https://github.com/sumanthshetty321/Sales-Data-Analysis/blob/main/Sales%20Data%20Analysis.pbix)



## Problem Statement

The business had sales data, but it needed a centralized and interactive way to understand product performance, profitability, sales trends, discount, customers and order detail and geographical performance.

The goal of dashboard was to convert raw data into meaningful insights that support better business decisions.


### Business Requirments
1)Top/Bottom 5 product by Sales/Profit/Quantity Sold.

2)How do sales trends vary over time (daily, monthly, quarterly, annually)?

3)Show relationship between sales and profit.

4)Compare sales/profit/quantity sold between any two periods selected by the user.

5)Average discount offered in each discount category.

6)Total number of orders.

7)Show Sales/Profit/Discount/Net Sales/All remaining fields for each order that could be filtered using visual filters (Product/Date/Customer ID/Promotion Categories).

8)Show sales by different cities.


### Steps followed 

- Step 1 : Loaded data into Power BI Desktop, dataset was in excel file with 4 different tables namely Dim Customers, Dim Products, Dim Promotion and Fact Table. Then Transformed data into Power Query Editor for cleaning and basic analysis
- Step 2 :In the Dim Promotion table, added a conditional column named 'Discount Percentage' using the PromotionID column, and then changed its data type to Whole Number.
 ![Discount Percentage Column](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Discount%20Percentage%20Column.png)

 
- Step 3 : In the Fact Table, several columns contained null values, including Price Per Unit, Total Sales, Discount Percentage, Discount Value, and Net Sales. Filled the missing values using Merge Queries and Custom Columns, changed the data types accordingly, and also added a Profit column.
    
      Price Per Unit = Merged Queries form Dim Product table
      Total Sales = [Unit Sold] * [Price Per Unit]
      Discount Percentage = Merged Queries form Dim Promotion table
      Discount Value = ([Total Sales] * [Discount Percentage])/100 
      Net Sales = [Total Sales] - [Discount Value]
      Profit = [Net Sales] * 0.10
    ![Nulls in Fact Table](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Nulls%20in%20Fact%20Table.png)
 



- Step 4 : In Report View, renamed Page 1 as “Top/Bottom 5” and created six bar charts to display the Top 5 and Bottom 5 products based on Sales, Profit, and Quantity Sold. For each chart, added Product Name and the respective measure to the Filters pane and applied the Top N filter to display the required products.

   ![Top N](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Top%20N.png)     
- Step 5 : In Report View, created a “Sales Trends” page and used a line chart with the Date hierarchy (Year, Quarter, Month, and Day) on the X-axis and Net Sales on the Y-axis to analyze sales trends over time.
   

- Step 6 : Created a bar chart using Promotion Name on the Y-axis and Average of Discount Percentage on the X-axis to compare the average discount offered across different promotions.
 ![Avg Discount](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Avg%20Discount.png)

- Step 7 : Created a scatter chart using Profit on the X-axis and Sales on the Y-axis to analyze the relationship between profit and sales.

  ![Profit vs Sales](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Profit%20vs%20Sales.png)     
       

        




- Step 8 : Created a Card visual using the Total Orders measure to display the overall number of orders.
  ![Total Orders](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Total%20Orders.png)

- Step 9 :Created a Map visual using City as the location and Net Sales as the bubble size to visualize sales performance across different cities.
    ![Sales by City](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Sales%20by%20city.png)

- Step 10 :Created a table visual to display detailed order-level information, including Customer ID, Date, Discount Percentage, Discount Value, Net Sales, Price per Unit, Product ID, Profit, Promotion ID, Total Sales, and Units Sold, with visual filters for interactive data analysis.

 
- Step 11 : Created two separate date tables called Date 1 and Date 2.
  
      Date 1 = CALENDERAUTO()
      Date 2 = CALENDERAUTO() 
    
- Step 12 : In Model View, connected the Date 1 table to the Fact Table with a 1:*  cardinality and kept the relationship active.
Connected the Date 2 table to the Fact Table with a 1:*  cardinality and kept the relationship inactive by unchecking “Make this relationship active.”
   ![Model View](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Model%20view.png)
- Step 13 :In Report View, created three measures for Total Sales, Total Profit, and Total Units Sold kept them in new table called '2p compare measure'.
Added two date slicers, one for Date 1 and another for Date 2, along with three clustered column charts to compare Sales, Profit, and Units Sold between the selected periods.
Added the corresponding measures to the Y-axis of each chart and configured the visuals for period-wise comparison.

      Total sales = CALCULATE(SUM('Fact Table'[Net Sales]),ALL('Date Table 1'),USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

      Total profit = CALCULATE(SUM('Fact Table'[Profit]),ALL('Date Table 1'),USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

      Quantity sold = CALCULATE(SUM('Fact Table'[Units Sold]),ALL('Date Table 1'),USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

        
 

 





 
 # Report Snapshot (Power BI DESKTOP)
### Overview:
![Overview](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Overview.png)


### Top/Bottom 5 product by Sales/Profit/Quantity Sold:

![Top & Bottom Products](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/5%20Top%20%26%20Bottom.png)

### Sales trends over time:

![Sales Trends](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Sales%20Trends.png)


###  Table Visual for all  fields for each order that could be filtered using   (Product/Date/Customer ID/Promotion Categories):

![Table Visual](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/Table%20Visual.png)



## Two Period Comparison of Sales/Profit/Quantity Sold:
#### [NOTE]:
Below both approaches produce the same output and visuals. Report 1 is recommended because it uses Power BI's built-in Edit Interactions feature from the Format tab, without requiring additional date tables or relationships. Report 2 achieves the same result by creating two separate date tables and establishing relationships with the Fact table. This approach adds unnecessary model complexity and can increase the model size and storage requirements.

### 1)

![Two Period Comparison 1](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/comparision1.png)

### 2)

![Two Period Comparison 2](https://raw.githubusercontent.com/sumanthshetty321/Sales-Data-Analysis/main/Screenshots/comparision2.png)



# Key Insights
 

### [1] Sales Trend:
 Sales declined from 31.4M in 2020 to 28.6M in 2022, a decrease of approximately 8.9%. 
 
 Sales then increased to 32.3M in 2023, representing an approximately 12.9% recovery from 2022.
### [2] Profit & Sales Relationship: 
The Profit vs Sales scatter plot shows a positive relationship between sales and profit, indicating that higher sales values are generally associated with higher profits.
### [3] Promotion Discounts: 
Weekend Flash Sale had the highest average discount at approximately 23K, followed by Clearance Sale (18K) and Summer Sale (7K).

 Weekend Flash Sale's average discount was approximately 27.8% higher than Clearance Sale and 228.6% higher than Summer Sale.
### [4] Total Orders: 
The dashboard recorded 3,510 total orders, providing an overview of the order volume across the analyzed period.
### [5] Geographical Performance: 
The Sales by Cities map shows that sales were distributed across multiple cities in India, allowing users to compare city-level sales performance.

### [6] Two-Period Comparison: 
The dashboard enables users to independently select two date ranges and compare Net Sales, Total Profit, and Units Sold, making it easier to measure changes between different periods.
