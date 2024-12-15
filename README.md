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



A. SELECT he.JobTitle, AVG(SickLeaveHours) AS SickLeave_Hrs

	FROM [HumanResources].[Employee]AS he
 
	INNER JOIN [HumanResources].[vEmployeeDepartment] AS hdv
 
	ON he.JobTitle = hdv.JobTitle
 
	GROUP BY he.JobTitle
 
	ORDER BY  SickLeave_Hrs DESC;
 

 B. select JobTitle, AVG(SickLeaveHours) as Avg_Sick_Leave
	from [HumanResources].[Employee]
	group by JobTitle
	order by Avg_Sick_Leave	DESC;
 

|JobTitle                         |SickLeave_Hrs |
|----------------------------     |--------------|
|Chief Executive Officer          |69            |
|Stocker                          |68            |
|Shipping and Receiving Clerk     |67            |
|Maintenance Supervisor           |66            |
|Shipping and Receiving Supervisor|66            |
Production Technician - WC10      |65            |
Janitor                           |64            |
Facilities Administrative Assistant|63       |
Facilities Manager|	63|
Quality Assurance Technician|	61|
Quality Assurance Supervisor|	60|
Quality Assurance Manager|	60|
Production Supervisor - WC60|	60|
Production Technician - WC45|	59|
Document Control Assistant|	59|
Production Supervisor - WC50|	58|
Document Control Manager|	58|
Research and Development Manager|	57|
Production Supervisor - WC45|	57|
Control Specialist|	57|
Application Specialist|	56|
Production Supervisor - WC40|	55|
Network Administrator	|54|
Network Manager|	54|
Production Supervisor - WC30|	54|
Database Administrator|	53|
Vice President of Production|	52|
Production Supervisor - WC10	|52|
Information Services Manager|	52|
Accounts Payable Specialist|	51|
Senior Tool Designer|	51|
Research and Development Engineer|	51|
Accounts Receivable Specialist|	50|
Accountant	|49|
Production Technician - WC40|	49|
Accounts Manager|	48|
Assistant to the Chief Financial Officer|	48|
Finance Manager|	47|
Buyer	|47|
Human Resources Manager|	47|
Human Resources Administrative Assistant|	46|
Purchasing Assistant	|45|
Benefits Specialist	|45|
Purchasing Manager	|44|
Recruiter	|44|
Production Technician - WC50	|43|
Scheduling Assistant	|43|
Master Scheduler	|42|
Marketing Specialist	|42|
Production Control Manager	|41|
Production Supervisor - WC20|	40|
Marketing Manager	|40|
Marketing Assistant	|40|
Production Technician - WC30|	36|
Sales Representative	|35|
Production Technician - WC60|	33|
European Sales Manager	|30|
Pacific Sales Manager	|30|
North American Sales Manager	|27|
Production Technician - WC20|	25|
Vice President of Sales|	25|
Tool Designer	|24|
Design Engineer|	22|
Engineering Manager	|21|
Senior Design Engineer	|21|
Chief Financial Officer	|20|
Vice President of Engineering|	20|


5. What is the relationship between store trading duration and revenue

SELECT YearOpened, ROUND((AVG(AnnualRevenue)/1000),2) AS Average_Revenue, COUNT(Name) AS Num_of_Stores

	FROM Sales.vStorewithDemographics
 
	GROUP BY YearOpened;
	

|YearOpened|Average_Revenue|Num_of_Stores|
|----------|---------------|-------------|
|1970	|5.79              |19	 	 |
|1971	|115.79	           |19		 |
|1972	|171.58	           |19		 |
|1973   |30.00		   |6		 |
|1974	|222.00	           |25 		 |
|1975|	120.80             |25		 |
|1976	|70.80		   |25	 	 |
1977	|225.00	 	   |12	 	 |
|1978	|137.60		   |25		 |
|1979	|199.20	 	   |25	 	 |
|1980	|222.00		   |25		 |
|1981	|165.00		   |12		 |
|1982	|	70.80	   |	25	 |
|1983	|	197.37	   |19	 	 |
|1984	|	137.60	   |25		 |
|1985 	|	115.00	   |	12	 |
|1986	|	222.00	   |	25	 |
|1987	|178.46		   |26		 |
|1988	|106.25		   |32		 |
|1989	|219.23		   |13		 |
|1990	|	143.85	   |26		 |
|1991	|	178.00	   |	20	 |
|1992	|222.22		   |27		 |
|1993	|	190.00	|14|
|1994	|98.15	|27|
|1995	|	200.00	|21|
|1996	|157.78	|27|
|1997	|	104.50	||20|
|1998	|	231.82	|33|
|1999	|	253.33|	33|
|2000	|90.00|	26|
|2001	|	100.00	|13|




6. What is the relationship between the size of the stores, number of employees and revenue


/* 6.What is the relationship between the size of the stores, number of employees and revenue?*/

		CREATE VIEW answer6 AS
	SELECT  SquareFeet AS Size, AVG(AnnualRevenue) AS Average_Revenue, AVG(NumberEmployees) AS Avg_num_employees
 
	FROM Sales.vStorewithDemographics
 
	GROUP BY SquareFeet

Commands completed successfully.

Completion time: 2024-12-15T23:08:23.6807694+00:00


|Size	|Average_Revenue|Avg_num_employees|
|-------|---------------|-----------------|
|6000	|30000.00	|3|
|7000	|30000.00	|5|
|8000	|30000.00	|5|
|9000	|30000.00	|5|
|10000	|30000.00	|5|
|11000	|30000.00	|7|
|17000	|80000.00	|10|
|18000	|80000.00	|13|
|19000	|80000.00	|15|
|20000	|80000.00	|14|
|21000	|80000.00	|14|
|22000	|80000.00	|15|
|23000	|80000.00	|18|
|24000	|100000.00	|24|
|25000	|100000.00	|24|
|26000	|100000.00	|24|
|27000	|100000.00	|23|
|28000	|100000.00	|27|
|35000	|150000.00	|32|
|36000	|150000.00	|35|
|37000	|150000.00	|38|
|38000	|150000.00	|41|
|39000	|150000.00	|39|
|40000	|150000.00	|44|
|41000	|150000.00	|45|
|42000	|150000.00	|48|
|68000	|300000.00	|52|
|69000	|300000.00	|57|
|70000	|300000.00	|58|
|71000	|300000.00	|62|
|73000	|300000.00	|73|
|74000	|300000.00	|76|
|75000	|300000.00	|87|
|77000	|300000.00	|89|
|78000	|300000.00	|92|
|79000	|300000.00	|94|
|80000	|300000.00	|97|









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
- reditcard
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
