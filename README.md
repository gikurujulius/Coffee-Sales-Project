# Coffee-Sales-Project 
## Step 1: Problem Statement
- Understand Sales Perfomance from the period 2019 to 2022
- Identify the top performing country sales for the period
- Track the sales of each coffee roast type per country
- Identify the top consumers.
- Identify top consumers for each coffee size.
- Identify the top consumers of each coffee roast type
- Analyze the consumption of the 3 roast types per size
- Identify the top valuable customers
- Track sales on customers with and without royalty cards.
- Track performance of each coffee size

## Step 2: Collect and gather the data
The coffeeOrdersData (raw).xlsx file contains the data used. The data contains the orders, customers and products tables.
1. On the orders table we are going to add the following columns
  - Customer Name
  -	Email
  - Country
  - Coffee Type
  - Roast Type
  -	Size
  - Unit Price
  - Sales
2. We utilize DXLOOKUP function to collect data from the customers table for the columns Customer Name, Email, and Country.
  - Under Customer Name, the formula,
    - =DXLOOKUP(C2,customers!$A$1:$A$1001,customers!$B$1:$B$1001,,0)
  - Under Email column, the data source has some empty rows. The formula 
    - =DXLOOKUP(C2,customers!$A$1:$A$1001, customers!$C$1:$C$1001,,0) gives a couple of zeros due to a lack of corresponding values. To eliminate this, IF statements come in handy.
    - =IF(DXLOOKUP(C2,customers!$A$1:$A$1001,customers!$C$1:$C$1001,,0)=0,"",DXLOOKUP(C2,customers!$A$1:$A$1001, customers!$C$1:$C$1001,,0))
  - Under the column Country we apply the formula
    - =DXLOOKUP(C2,customers!$A$2:$A$1001, customers!$G$2:$G$1001,,0)
3. Next, we source information from the products table for the remaining columns. Utilizing index match since it will be dynamic.
  - =INDEX(products!$A$1:$G$49,MATCH(orders!$D2,products!$A$1:$A$49,0),MATCH(orders!I$1,products!$A$1:$G$1,0))
    
4. The sales values are derived from the unit price * quantity.

## Step 3: Data Wrangling and Formatting
1. Add column Coffee Type name to reflect the full name of the coffee types utilizing the formula
  - =IF(I2="Rob","Robusta",IF(I2="Exc","Excelsa", IF(I2="Ara", "Arabica",IF(I2="Lib","Liberica",""))))
Rob reflects to Robusta, Exc to Excelsa, Ara to Arabica and Lib to Liberica.
2. Add column Roast type Name to reflect the full name of the roast type.
M refers to Medium
L refers to Light
D refers to Dark
  - •	=IF(J2="M","Medium",IF(J2="L", "Light",IF(J2="D","Dark","")))
3. Format Order date column to reflect the date format dd-mmm-yyyy
4. Add the metric in the Size column while keeping a one decimal place. In this scenario the metric is “Kg”
5. Format the columns Unit Price and Sales into USD currency.
6. Check for duplicates in the data

## Pivot Tables, Charts, Findings and Dashboard
Coffee Sales Dashboard.png file is the dahsboard.





