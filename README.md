## Data Warehouse Design for E-commerce Environments

### AIM: 
```
To construct a data warehouse for a retail e-commerce store in this project. You would also be expected to answer a few
particular issues about pricing optimization and inventory allocation in terms of design and implementation. In this
project, you'll be attempting to answer the following two questions:

-	Were the higher-priced items more prevalent in some markets?
-	Should inventory be reallocated or prices adjusted based on location?
```

### INTRODUCTION:

#### Definition:
```
The primary concept of data warehousing is that the data stored for business analysis can most effectively be accessed by separating 
it from the data in the operational systems. A data warehouse is a collection of computer-based information that is critical to 
successful execution of enterprise initiatives. A data warehouse is more than an archive for corporate data and more than a new way 
of accessing corporate data. A data warehouse is a subject-oriented repository designed with enterprise-wide access in mind. 
It providestools to satisfy the information needs of the employees organizational levels-not just for complex data queries, but
as general facilityfor getting quick, accurate and often insightfulinformation. A data warehouse is designed so that its users 
can recognize the informationthey want and access that information using simple tools.

One of the principal reasons for developing a data warehouse is to integrate operational data from various sources into a single
and consistent architecture that supports analysis and decision-making within the enterprise. Operational systems create, update
and delete production data that feed the data warehouse. A data warehouse is analogous to a physical warehouse. Operational systems
create data ‘parts’ that are loaded into the warehouse. Some of those parts are summarised into information ‘components’ and are 
stored in the warehouse. Data warehouse users make requests and are delivered information ‘products’ that are created from the 
components and parts stored in the warehouse. A data warehouse is typically a blending of technologies, including relational 
and multidimensional databases,client/ server architecture, extraction / transformation programs, graphical user interfaces,
and more.
```
### ELT vs ETL DIAGRAM:

![elt vs etl](https://user-images.githubusercontent.com/74660507/232379648-14faae15-4a1e-4333-a95d-a95dee2da646.png)

#### DATA PIPELINE MODEL:

![image](https://user-images.githubusercontent.com/74660507/232360360-ccb6db2b-5593-4cb6-81fa-2218cfa1c1cc.png)

#### LOGICAL DATA MODEL:

![image](https://user-images.githubusercontent.com/74660507/232360594-9d1f1980-7a91-4322-8e20-13c7d54b1c72.png)

#### REPORTING DATA MODEL:

![image](https://user-images.githubusercontent.com/74660507/232360750-4c9edb5e-afed-49ee-856f-31055ffeaafe.png)

#### CONTENTS:
```
In this project, we'll be creating the Data Warehouse and Data Pipeline using the Excel Power Query. We can also use tools
like AWS Cloud, Microsoft SQL Server Management Studio, Power BI or Ploomberg to create the Pipleine.
```

#### SOFTWARE REQUIREMENTS:
```
1. Microsoft Excel
or
2. Power BI
or
3. AWS Cloud
or
4. Microsoft SQL Server Management Studio
```

#### Steps:

1. Create and Extract DataBase Tables with Dimensions for the E-commerce sales in the Microsoft excel or Power BI/ Microsoft SQL Server Management Studio/ AWS Cloud

a. EXCEL

#### DATA TABLE:

![image](https://user-images.githubusercontent.com/74660507/232362821-e897c172-9794-4e02-adbb-687644e31558.png)

#### QUERIES & CONNECTIONS:

![image](https://user-images.githubusercontent.com/74660507/232363401-1d8f607f-00be-492d-bfaf-2d3f72d2f67b.png)

b. MICROSOFT SQL SERVER MANAGEMENT STUDIO
```SQL
Createdatabase Retail_DW
Go

Use Retail_DW
Go

Create table DimProduct
(
ProductKey int primary key identity,
ProductAltKey varchar(10)not null,
ProductName varchar(100),
ProductActualCost money,
ProductSalesCost money

)
Go
Create table DimOrder
(
StoreID int primary key identity,
StoreAltID varchar(10)not null,
StoreName varchar(100),
StoreLocation varchar(100),
City varchar(100),
State varchar(100),
Country varchar(100)
)
Go
```
c. AWS CLOUD
```
$ python create_tables.py
```
2. Transform the data base tables, merge the dimensions with the fact tables of the data base

a. EXCEL

#### PRODUCT DIMENSION TRANSFORMED:

![image](https://user-images.githubusercontent.com/74660507/232364089-201a5c60-3f27-49e8-8bc2-38a0ace85873.png)

#### ORDER FACT TRANSFORMED:

![image](https://user-images.githubusercontent.com/74660507/232364510-9ed3e5f1-442c-4def-8df8-d95f8c9cb9bb.png)

#### CUSTOM COLUMN TRANSFORMED:

![image](https://user-images.githubusercontent.com/74660507/232364582-02f1b580-2695-4621-8759-66d5d669a10d.png)

#### TOTAL SALES TRANSFORMED:

![image](https://user-images.githubusercontent.com/74660507/232365320-8ea45899-cd69-4c8d-8cb4-057e0a4d9449.png)

#### TOTAL SALES LOADED:

![image](https://user-images.githubusercontent.com/74660507/232365402-b12a20ad-d7bc-4de8-b2c9-1e7be2315897.png)

b. MICROSOFT SQL SERVER MANAGEMENT STUDIO
```SQL

Create Table FactProduct
(
TransactionId bigint primary key identity,
SalesInvoiceNumber int not null,
SalesDateKey int,
SalesTimeKey int,
SalesTimeAltKey int,
StoreID int not null,
CustomerID int not null,
ProductID int not null,
SalesPersonID int not null,
Quantity float,
SalesTotalCost money,
ProductActualCost money,
Deviation float
)

```
c. AWS CLOUD
```
$ python etl.py
```

3. Visualaize and get the report of the data using Chart or Power BI 

#### QUERY DEPENDENCIES:

![query dependencies](https://user-images.githubusercontent.com/74660507/232379743-6a7d105d-127f-4fef-9d00-26a2feaa012c.png)

#### DATA MODEL:

![image](https://user-images.githubusercontent.com/74660507/232368039-959ac721-e1d6-4c7c-afe8-64bc3e354d9d.png)

#### VISUALIZATION OF PRODUCT ID, CATEGORY NAME & PRODUCT NAME:

![image](https://user-images.githubusercontent.com/74660507/232370391-f95243c5-e8da-4be5-9026-a8f911c6c40f.png)

#### VISUALIZATION OF COUNT OF SALES AMOUNT:

![image](https://user-images.githubusercontent.com/74660507/232370678-3a08e9d5-9ff6-41ba-a532-51c211756b5e.png)

#### VISUALIZATION OF TOTAL SALES & CATEGORY NAME:

![image](https://user-images.githubusercontent.com/74660507/232369128-2a355e88-49aa-4f32-ba02-146dc257c655.png)

#### PIVOT TABLE OF TOTAL SALES:

![image](https://user-images.githubusercontent.com/74660507/232369212-53c82fc6-60db-472f-906b-b6337e8aa367.png)

4. The created Pipeline Model can be used for further Machine Learning algorithms using the Cloud servers.

### CONCLUSION:

-	Were the higher-priced items more prevalent in some markets? <br>
  Yes, higher-priced items are more prevalent in some markets because of the quality and interest of the customers.
  
-	Should inventory be reallocated or prices adjusted based on location? <br>
  No, inventory does'nt have to be re-allocated for the prices. Prices should be adjusted based on the location and the currency used by the country.
  
### RESULT:
Thus, a Data Warehouse and a ETL Data Pipeline is created using the Excel Power Query for Data Warehouse Design for E-commerce Environments.
