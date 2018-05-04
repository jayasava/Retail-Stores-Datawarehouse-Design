# Retail-Stores-Datawarehouse-Design
(Inspired and followed Ralph Kimball Datawarehouse kit)

### 1. Point of Sales(POS) system:
The Operational system of Retail system is Transaction based and on scanning the barcode of products, following details are captured.
(POS diagram)

                                                    Organization Name
                                               Address Line1, Address Line2,
                                                  City, State, Zip code
                                                     Phone Number


Store Number: S1    
POS Cashier: C1

|ProductKey|ProductShortName|Quantity|Actual Price|Discount|Net Price|
|----------|----------------|--------|------------|--------|---------|



                                |TotalItems:      |Total Amount:   |You Save:   | You Owe:    |
          
                 Paid by: Cash/Card

         
  Transaction ID:  12345678910110013227
  
  
-------------------------------------------------------------------------------------------------------------------------------  

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
![Link](https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Schemas/Schema_Initial.png)

### 6. Desigining Dimensions:
Note: 
Attributes for a given dimension depends on the business requirement and varies from one organization to others.
Listed attributes are considered basic ,important and found in almost all organizations
   #### Date Dimension:
   
    Time of the Day is not considered aa a Measure of Dimension in order to avoid Data Explosion
 Link to Fields: 
    https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/Date/
  
   #### Product Dimension:
     Considering the categoriation of products to be:
     Stores -> Departments -> Categories -> SubCategories -> Brand -> Individual Products
     
     Apart from Product Key, Considering even Stock Key Unit (SKU) which is a machine identifiable barcode 
     assigned to a product in order to track the item for inventory ( is in stock/ needs reordering).
     SKU( about 8 characters) reveals product details such as color, size, manufacturer,brand etc., This 
     will help place different products of same category together and while customers chose a product online
     SKU will help to show suggestions related to same category.
     
 Link to Fields: 
     https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/Product/
     
   #### Store Dimension:
  Link to Fields: 
     https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/Store/
     
   #### Promotion Dimension:
    Promotion Dimension is a Casual Dimension as it(or its attributes) has an impact on operation. 
       It is used to analyze:
       
       1. Lift - Gain in sales during promotional period (Sales during promotion period - base 
       sales before promotion from history)
       2. Cannibalization - Decrease in sales of products in same category
       3. Time Shifting - Negating gain in sales due to drop in sales just before or after Promotion period
       4. Overall gain in sales
    -> If multiple promotions can be applied on a product, then casual dimensions are to be placed in different
    dimensions.
    -> In case no promotion is applied on the product , then to preserve referential integrity , including an 
    entry in Promotion Dimension to hold No promotion entry.
  Link to Fields: 
     https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/Promotion/
     
   #### Cashier Dimension:
  Link to Fields: 
     https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/Cashier/
   #### PaymentMethod Dimension:
  Link to Fields: 
     https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Dimensions/PaymentMethod/
 
 ### 7. Star Schema in Action:
 ![Link](https://github.com/jayasava/Retail-Stores-Datawarehouse-Design/blob/master/Schemas/StarSchema.PNG)
 
 ### 8. Degenerate Dimensions:
 
* Every row in the Fact Table consists of Product purchased along with the POS Transaction Number. Transaction Number together with ProductKey serves as a Primary Key to the Fact Table.
* The Transaction Number is used as a Grouping Key to pull all the purchases under single transaction and also to link to Operational system.
* Transaction Number is a Dimension Key but as it doesnt have any other attributes supporting it , thus, No Dimension is required and is referred to ad Degenerate Dimension. It stays in Fact Table and doesnt join with any Dimension Table.
   
   
      
     


