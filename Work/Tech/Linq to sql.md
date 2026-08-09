[Linq to sql](https://learn.microsoft.com/en-us/dotnet/framework/data/adonet/sql/linq/)
[linq to sql connection strings](https://weblogs.asp.net/rajbk/Contents/Item/Display/425/)

#### Fix for creating new stored procedures and trying to make them available via linq to sql

1. for every return value (out parameter) stub them out with a fake if block like so 
```sql
IF 1 = 0
BEGIN
	SELECT
		CAST(NULL AS INT) AS ID,
		CAST(NULL AS VARCHAR(100)) AS NAME
	RETURN
END
```
2. add it to the top of the stored procedure you are dragging
3. drag the stored procedure to linq to sql and fix issues that come up
4. remove stubbed if block after success
5. rerun stored procedure.