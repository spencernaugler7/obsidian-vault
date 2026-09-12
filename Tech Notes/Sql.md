## Find tables with column name
Tsql
```sql
select t.name as TableName, c.name as ColumnName
from sys.columns c
inner join sys.tables t on t.object_id = c.object_id
where c.name like '<table_name>'
```

## Special var's/functions

[`@@rowcount`](https://learn.microsoft.com/en-us/sql/t-sql/functions/rowcount-transact-sql?view=sql-server-ver17) Returns the number of rows affected by the last statement
[`SCOPE_IDENTITY()`](https://learn.microsoft.com/en-us/sql/t-sql/functions/scope-identity-transact-sql?view=sql-server-ver17) Returns the last identity value inserted into an identity column in the same scope

## Types
`uniqueidentifier`16-byte GUID [uniqueIdentitfyer](https://learn.microsoft.com/en-us/sql/t-sql/data-types/uniqueidentifier-transact-sql?view=sql-server-ver17)

## Tsql jobs
- [add job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql?view=sql-server-ver17)
- [add step to a job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql?view=sql-server-ver17)
- [add schedule to a job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql?view=sql-server-ver17)
- [add job to server](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql?view=sql-server-ver17)

## Insert
```sql
INSERT INTO Production.UnitMeasure  
VALUES 
	(N'FT2', N'Square Feet ', '20080923'), 
	(N'Y', N'Yards', '20080923'), 
	(N'Y3', N'Cubic Yards', '20080923');
```

## Insert With Select
```sql
INSERT INTO dbo.EmployeeSales 
SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD 
FROM Sales.SalesPerson AS sp 
INNER JOIN Person.Person AS c ON sp.BusinessEntityID = c.BusinessEntityID WHERE sp.BusinessEntityID LIKE '2%' 
ORDER BY sp.BusinessEntityID, c.LastName;
```

## Declare Function
functions can be scalar valued (returns a single value), or table valued (returns a table)
###### scalar value
```sql
CREATE FUNCTION CtrAmount ( @Ctr_Id int(10) )
  RETURNS MONEY
  AS
  BEGIN
      DECLARE @CtrPrice MONEY
        SELECT @CtrPrice = SUM(amount)
          FROM Contracts
        WHERE contract_id = @Ctr_Id
      RETURN(@CtrPrice)
  END
GO 
```
###### table valued
```sql
CREATE FUNCTION function_name (@PRODUCT_ID Int)
  RETURNS @ProductsList Table
    (Product_Id Int,
     Product_Dsp nvarchar(150),
     Product_Price Money )
AS
  BEGIN
    IF @PRODUCT_ID IS NULL
      BEGIN
        INSERT INTO @ProductsList (Product_Id, Product_Dsp, Product_Price)
        SELECT Product_Id, Product_Dsp, Product_Price
        FROM Products
      END
    ELSE
      BEGIN
        INSERT INTO @ProductsList (Product_Id, Product_Dsp, Product_Price)
        SELECT Product_Id, Product_Dsp, Product_Price
        FROM Products
        WHERE Product_Id = @PRODUCT_ID
      END
    RETURN
  END
GO
```
## Execute function
###### scalar valued
```sql
declare @languageId int = 0
exec @languageId = sfn_GetLanguageById @RequestId = 4
select @languageId
```
###### table valued
```sql
select * from tfn_RequestNeedToCreateCernerDoc()
```

## Declare stored procedure
```sql
CREATE PROCEDURE SalesLT.uspGetCustomerCompany
(
    @LastName nvarchar(50) = NULL, -- default value
    @FirstName nvarchar(50) = NULL,
    @CompanyUserId int output -- output value this is how you can return values
)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON

    -- Insert statements for procedure here
    SELECT FirstName, LastName, CompanyName
       FROM SalesLT.Customer
       WHERE FirstName = @FirstName AND LastName = @LastName;
    
    -- set output parameters in any select
    select @CompanyUserId = c.CompanyUserId
    from SalesLt.Company c
    where c.Id = 1
END
GO
```

## Execute stored procedure
```sql
-- declare the output variable
DECLARE @MyOutputParameter INT;

-- execute the stored procedure without parameter's names
EXEC my_stored_procedure 'param1Value', @MyOutputParameter OUTPUT

-- or execute the stored procedure with parameter's names
EXEC my_stored_procedure @param1 = 'param1Value', @myoutput = @MyOutputParameter OUTPUT

-- see output
select @MyOutputParameter
```
