# Cookbook
## Find tables with column name
Tsql
```sql
select t.name as TableName, c.name as ColumnName
from sys.columns c
inner join sys.tables t on t.object_id = c.object_id
where c.name like '<table_name>'
```

# Special var's/functions

[`@@rowcount`](https://learn.microsoft.com/en-us/sql/t-sql/functions/rowcount-transact-sql?view=sql-server-ver17) Returns the number of rows affected by the last statement

[`SCOPE_IDENTITY()`](https://learn.microsoft.com/en-us/sql/t-sql/functions/scope-identity-transact-sql?view=sql-server-ver17) Returns the last identity value inserted into an identity column in the same scope

## Types
`uniqueidentifier`16-byte GUID [uniqueIdentitfyer](https://learn.microsoft.com/en-us/sql/t-sql/data-types/uniqueidentifier-transact-sql?view=sql-server-ver17)

## Tsql jobs
- [add job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql?view=sql-server-ver17)
- [add step to a job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql?view=sql-server-ver17)
- [add schedule to a job](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql?view=sql-server-ver17)
- [add job to server](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql?view=sql-server-ver17)