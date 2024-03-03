# Superstore Analysis Dashboard

![c3478510_1](https://github.com/nehapereira/Superstore-Power-BI-Analysis/assets/136058806/78b896f2-e467-4e6e-ba56-2c019fc3a5c0)
![c3478510_2](https://github.com/nehapereira/Superstore-Power-BI-Analysis/assets/136058806/9815cfb2-0561-4327-8fcc-d55cd7283136)
![c3478510_3](https://github.com/nehapereira/Superstore-Power-BI-Analysis/assets/136058806/d536eb84-2aa3-4200-a63c-cf86249bb0e5)
![c3478510_4](https://github.com/nehapereira/Superstore-Power-BI-Analysis/assets/136058806/a00bd89c-49a0-4267-8bac-1f9e10787263)


## Dataset: [Superstore Dataset on Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

## Problem Statement

This is an analysis of the superstore dataset from Kaggle as linked above. As seen in the screenshots in the year slicer this shows data for 2016. 
It details total sales, profits, gross margin percentages, and year-over-year sales growth.
It also segments data by consumer groups, product categories (Technology, Furniture, Office Supplies), and geographical regions (West, East, Central, South), offering insights into the performance metrics like total orders and sales by quarter. 

## DAX Measures

Total Sales = SUM(Superstore[Sales])

Total Profit = SUM(Superstore[Profit])

Gross Margin % = DIVIDE([Total Profit],[Total Sales], 0.0)

Sales Growth = 
VAR CurrentYearSales = [Total Sales]
VAR PreviousYearSales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
RETURN
IF(ISBLANK(PreviousYearSales), 0.0, (CurrentYearSales - PreviousYearSales) / PreviousYearSales)

Total Orders = COUNTROWS(Superstore)

Avg Order-to-Ship Days = 
AVERAGEX(
    SUMMARIZE('Superstore', 'Superstore'[Product ID]),
    DATEDIFF(
        MIN('Superstore'[Order Date]),
        MIN('Superstore'[Ship Date]),
        DAY
    )
)
