# Sale Overview Analysis

### Dashboard Link : https://app.powerbi.com/groups/me/reports/29636afd-664b-4322-a97f-20a38d17d565/4560add4c8387208d437?experience=power-bi

## Problem Statement

This dashboard helps to tracks key metrics—Sales, Profit and Quantity—across four regions: Central, East, South, and West. The dashboard allow users to filter by year and dynamically switch between the three metrics (Sales, Profit and Quantity). Additionally, it includes a comparison with the previous year's (PY) sales for the selected year.
Since, number of neutral/dissatisfied customers (almost 57 %) are more than satisfied customers (around 43 %), thus in all they must work on improving their services. 


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : It was observed that in none of the columns errors & empty values were present.

- Step 4 : Create a calendar table and do data modelling(to get current year and previous year metrics).
           Under Table View in table tools click New Table to create Calendar Table.
           Under Table View in table tools click New column to create Year and Month Columns.

           Calendar Table = CALENDAR(MIN('Sales Data'[Order Date]),MAX('Sales Data'[Order Date]))
           Year = YEAR('Calendar Table'[Date])
           Month = FORMAT('Calendar Table'[Date],"mmm")
           
           Under Model View make connection between the tables(Order date column in sales table and date column in 
           Calendar table with cardinality One-to-many.   

- Step 5 : Under Report View , Visualizations add Canvas Background with 0% transparency.
 
- Step 6 : Create a new measure for Total Sales, Total Profits, Total Quantity.

           Total Sales = sum('Sales Data'[Sales])
           Total Quantity = SUM('Sales Data'[Quantity]) 
           Total Profits = sum('Sales Data'[Profit])

- Step 7 : Under Modeling, create new parameter to switch between Total Sales, Total Profits and Total Qty.

![Parameter](https://github.com/user-attachments/assets/9c00d600-b4e3-4b69-93f7-57a87f72b194)

- Step 8 : Under Report View, add KPI and in parameter select total sales and drag parameter to KPI fields ,Add Text box and add text central, format KPI and Text box.

- Step 9 : Under Report View, add Slicer and drag Year to fields and format the slicer.

- Step 10 : Create new measure for Dynamic Title for dynamic selection between Sales, Profit, and Quantity. And add KPI 
            card to the Dynamic Title.

            Dynamic Title = max(Parameter[Parameter]) 

- Step 11 : To show Sales for the previous year based on the selected year create a new measure. And add KPI card to  
           PY KPI Sales

           PY KPI Sales = 
                    VAR SelectedYear = SELECTEDVALUE('Calendar Table'[Year])
                    VAR PerviousYearSales = CALCULATE([Total Sales],'Calendar Table'[Year]=SelectedYear - 1)
                    Var FORMATPYSLAES =FORMAT(PerviousYearSales/1000,"0.00")
                    return
                    if(ISBLANK(PerviousYearSales),"PY KPI Sales: No Data","PY Sales:" & FORMATPYSLAES & "K")

- Step 12 :Add column to Calendar Table to get month number. Add clustered column chart and drag month to x-axis and drag
          parameter to y-axis. Select Month column and in column tool sort by Month Number.
          Add average line to the chart 

          Month Number = MONTH('Calendar Table'[Date])

Make sure to apply central region under filer in filters on in visual block.
![central](https://github.com/user-attachments/assets/e5e63a9f-0b24-4f57-9295-1d2f8dcbc32d)

Same way add all the format to EAST,WEST,SOUTH regions and apply all the formats required.

![regions](https://github.com/user-attachments/assets/143e71c8-e31f-44f1-9f19-8fe100d3666f)


- Step 13 : select Map and drag state/Provision to location , region to legend, parameter to bubble size.
            Create new measure for DynamicMapTitle for dynamic title for Sales, Profit, and Quantity.

            DynamicMapTitle = max(Parameter[Parameter])& " by State"
Add DynamicMapTitle measure in title under visualization ,general tab.

![map](https://github.com/user-attachments/assets/cab69ba7-24c2-4396-afb1-fb68ef3c52c8)


- Step 14 : select stacked bar chart and drag state/province to y-axis, parameter to x-axis and region to legend and format the chart.

![stacked](https://github.com/user-attachments/assets/5b2bd418-0480-4a7c-81ec-dfe08a69875c)

- Step 15 : Create new measure for the following :

             CY Sales: Current Year Sales
                      CY Sales = 
                                 VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                 VAR CurrentYearSales = CALCULATE([Total Sales],'Calendar Table'[Year]=SelectedYEAR)
                                 RETURN CurrentYearSales

             PY Sales: Previous Year Sales
                      PY Sales = 
                                 VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                 VAR PreviousYearSales = CALCULATE([Total Sales],'Calendar Table'[Year]=SelectedYEAR-1)
                                 RETURN if(ISBLANK(PreviousYearSales),"No Data",PreviousYearSales)


             YoY Sales: Year-over-Year Sales growth or decline
                      YoY Sales = 
                                  var CurrentYearSales = [CY Sales]
                                  VAR PreviousYearSales = [PY Sales]
                                  VAR IsText = NOT(ISNUMBER(PreviousYearSales))
                                  Var YoYchange = if(IsText,"No Data",DIVIDE(CurrentYearSales-PreviousYearSales,PreviousYearSales))
                                  var print = if(YoYchange > 0 ,UNICHAR(9650) & " " & FORMAT(YoYchange,"0%"),
                                                                UNICHAR(9660) & " " & FORMAT(YoYchange,"0%"))
                                                                RETURN print


             CY Profit: Current Year Profit
                       CY Profit = 
                                  VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                  VAR CurrentYearProfits = CALCULATE([Total Profits],'Calendar Table'[Year]=SelectedYEAR)
                                  RETURN CurrentYearProfits


             PY Profit: Previous Year Profit
                       PY Profit = 
                                  VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                  VAR PreviousYearProfit = CALCULATE([Total Profits],'Calendar Table'[Year]=SelectedYEAR-1)
                                  RETURN if(ISBLANK(PreviousYearProfit),"No Data",PreviousYearProfit)


             YoY Profit: Year-over-Year Profit growth or decline
                       YoY Profits = 
                                     var CurrentYearProfit = [CY Profit]
                                     VAR PreviousYearProfit = [PY Profit]
                                     VAR IsText = not(ISNUMBER(PreviousYearProfit))
                                     Var YoYchange = if(IsText,"No Data",DIVIDE(CurrentYearProfit-PreviousYearProfit,PreviousYearProfit))
                                     var print = if(YoYchange > 0 ,UNICHAR(9650) & " " & FORMAT(YoYchange,"0%"),
                                     UNICHAR(9660) & " " & FORMAT(YoYchange,"0%"))
                                     return print


             CY Qty: Current Year Quantity
                       CY Quantity = 
                                    VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                    VAR CurrentYearQuantity = CALCULATE([Total Quantity],'Calendar Table'[Year]=SelectedYEAR)
                                    RETURN CurrentYearQuantity


             PY Qty: Previous Year Quantity
                       PY Qty = 
                                VAR SelectedYEAR = SELECTEDVALUE('Calendar Table'[Year])
                                VAR PreviousYearSales = CALCULATE([Total Quantity],'Calendar Table'[Year]=SelectedYEAR-1)
                                RETURN if(ISBLANK(PreviousYearSales),"No Data",PreviousYearSales)


             YoY Qty: Year-over-Year Quantity growth or decline
                       YoY Qty = 
                                 var CurrentYearQty = [CY Qty]
                                 VAR PreviousYearQty = [PY Qty]
                                 var IsText = not(ISNUMBER(PreviousYearQty))
                                 Var YoYchange = if(IsText,"No Data",DIVIDE(CurrentYearQty-PreviousYearQty,PreviousYearQty))
                                 var print = if(YoYchange > 0 ,UNICHAR(9650) & " " & FORMAT(YoYchange,"0%"),
                                 UNICHAR(9660) & " " & FORMAT(YoYchange,"0%"))
                                 return print

![report](https://github.com/user-attachments/assets/9f3eef0e-1a1d-4bb6-983a-3e0d03c165f1)







