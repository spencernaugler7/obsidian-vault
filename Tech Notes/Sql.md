# Find tables with column name
Tsql
```sql
select t.name as TableName, c.name as ColumnName
from sys.columns c
inner join sys.tables t on t.object_id = c.object_id
where c.name like '<table_name>'
```
