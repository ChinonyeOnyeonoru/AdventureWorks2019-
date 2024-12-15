# AdventureWorks2019-
The AdventureWorks demo database 

## Objectives ans Solutions 

1. What is the regional sales in best performing country
### Query

/****** Script for SelectTopNRows command from SSMS  ******/

SELECT Name as Region_name, Round(SalesYTD,2) as YTD,Round(SalesLastYear,2) 
as LastYear 

from Sales.SalesTerritory

where CountryRegionCode = 'US'

order by (SalesYTD + SalesLastYear) desc


|Region_name|YTD        |LastYear   |
|-----------|-----------|-----------|
|Southwest  |10510853.87|5366575.71 |
|Northwest  |	7887186.79|3298694.49 |
|Southeast  |2538667.25 |3925071.43 |
|Central    |	3072175.12|3205014.08 |
|Northeast  |	2402176.85|3607148.94 |

   
2. What is the relationship between annual leave taken and bonus


select VacationHours as Annual_leave_hrs, e.BusinessEntityID, s.bonus

	from[HumanResources].[Employee] as e
 
	inner join [Sales].[SalesPerson] as s
 
	on e.BusinessEntityID = s.BusinessEntityID

create view leave_bonus as
 
	select VacationHours as Annual_leave_hrs , bonus
 
	from[HumanResources].[Employee] as e
 
	inner join [Sales].[SalesPerson] as s
 
	on e.BusinessEntityID = s.BusinessEntityID

|Annual_leave_hrs|BusinessEntityID|bonus|
|----------------|----------------|----------------|
|14|274|0.00|
|38|275|4100.00|
|27|276|2000.00|
|24|277|2500.00|
|33|278|500.00|
|29|279|6700.00|
|22|280|5000.00|
|26|281|3550.00|
|31|282|5000.00|
|23|283|3500.00|
|39|284|3900.00|
|20|285|0.00|
|36|286|5650.00|
|21|287|0.00|
|35|288|75.00|
|37|289|5150.00|
|34|290|985.00|

3. What is the relationship between Country and Revenue

select CountryRegionName as country , round((sum(AnnualRevenue)/1000000),2)as Revenue

	from [Sales].[vStoreWithAddresses]as s1
 
	inner join [Sales].[vStoreWithDemographics]as s2
 
	on s1.BusinessEntityID = s2.BusinessEntityID
 
	group by CountryRegionName
 

|Country|Revenue|
|--------|-------|
|Australia|6.42|
|Canada|18.04|
|Germany|5.90|
|France|6.65|
|United Kingdom|6.80|
|United States|68.98|


4. What is the relationship between sick leave and Job Title (PersonType)

select JobTitle, AVG(SickLeaveHours) as Avg_Sick_Leave,OrganizationLevel
	from [HumanResources].[Employee]
	group by JobTitle,OrganizationLevel




5. What is the relationship between store trading duration and revenue
6. What is the relationship between the size of the stores, number of employees and revenue
7. 







### Schema:humanresources 
- department
- employee
- employeedepartmenthistory
- employeepayhistory
- jobcandidate
- shift

## ER Diagram of humanresources Schema:
![image](https://github.com/user-attachments/assets/943d301e-efad-4b78-82bb-31cd0377f39e)


Schema: person:
- address
- addresstype
- businessentity
- businessentityaddress
- businessentitycontact
- contacttype
- countryregion
- emailaddress
- person
- personphone
- phonenumbertype
- stateprovince

  ## ER Diagram of person Schema

![image](https://github.com/user-attachments/assets/17451158-b063-4e37-9c69-ad7bbfe62d5c)

## Schema: production

- BillOfMaterials
- Culture
- Document
- Illustration
- Location
- Product
-ProductCategory
- ProductCostHistory
- ProductDescription
- ProductDocument
- ProductInventory
- ProductListPriceHistory
- ProductModel
- ProductModelIllustration
- ProductModelProductDescriptionCulture
- ProductPhoto
- ProductProductPhoto
- ProductReview
- ProductSubcategory
- ScrapReason
- TransactionHistory
- TransactionHistoryArchive
- UnitMeasure
- WorkOrder
- WorkOrderRouting


### ER Diagram of production Schema

![image](https://github.com/user-attachments/assets/a8fa1327-96ea-42e1-a905-4ae738d76681)


## Schema: purchasing

- purchaseorderdetail
- purchaseorderheader
- shipmethod
- vendor
- productvendor

### ER Diagram of purchasing Schema:

![image](https://github.com/user-attachments/assets/0e4837ab-bea0-4c59-b650-3beebd38cca0)

## Schema: sales

- salesorderheadersalesreason
- customer
- countryregioncurrency
- currencyrate
 -  reditcard
- specialoffer
- specialofferproduct
- currency
- store
- personcreditcard
- salestaxrate
- salespersonquotahistory
- salesreason
- salesterritoryhistory
- salesterritory
- salesperson
- salesorderheader
- salesorderdetail
- shoppingcartitem
  
### ER Diagram of sales Schema:

![image](https://github.com/user-attachments/assets/7e123a9f-4143-440c-8f83-dc0d0879ad4f)
