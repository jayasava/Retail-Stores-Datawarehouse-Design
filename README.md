# Retail-Stores-Datawarehouse-Design

### 1. Point of Sales(POS) system:
The Operational system of Retail system is Transaction based and on scanning the barcode of products, following details are captured.
(POS diagram)

### 2. Business Process(Operational System):
To Capture Purchases of Customers at POS and impact of Promotions on sales

### 3. Grain Declaration of Fact Table:
The Operational System captures Lowest Grain/ Atomic data ie., Each row has single Item bought on a particular day.
This can be used to find difference in sales daily/weekly/monthly/yearly

### 4. Designing Dimensions:

Dimensions required as per Operational System:

Date|
Store(again has Location dimension)|
Cashier|
Product|
Promotions|
MethodOfPayment|

### 5. Identifying Facts:
Fact Table consists of One product per line.
Facts would be - 
1. Quantity of product bought
2. Actual Price of Product per Unit
3. Actual Amount = Quantity of product bought * Actual Price of Product Per Unit
4. Discount on Product per Unit
5. Total Discount = Quantity of Product bought * Discount on Product per Unit
6. Net Amount = Actual Amount - Total Discount
7. Standard Cost of Product per Unit
8. Total Standard Cost = Standard Cost of Product per Unit * Quantity of product bought
9. Gross Profit = Total Standard Cost - Net Amount

#### Intial Retail Stores Schema
<img src = https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Schemas/Schema_1.png width="100 height= "100">



