# Basic Commands

Add  and update recodes

```sql title="Add recodes to database"
INSERT INTO DB_NAME.TABLE_NAME (column1, column2) VALUES(value1, value2)
```

```sql title="Update recodes in database"
UPDATE DB_NAME.TABLE_NAME set column1=value1 WHERE column2=some_value
```

```sql title="Get table size"
SELECT
    table_name AS `Table`,
    round(((data_length + index_length) / 1024 / 1024), 2) `Size in MB`
FROM information_schema.TABLES
WHERE table_schema = "DATABASE_NAME"
    AND table_name = "TABLE_NAME";
```

```bash title="Run mysqldumb"
mysqldump -h _MYSQL_HOST_ --port _PORT_ -u _USERNAME_ -p --skip-column-statistics _DB_NAME_ > mydump.sql
```

```bash title="Run mysql restore"
mysql -h _MYSQL_HOST_  --port _PORT_ -u <USERNAME> -p < mydump.sql
```

```sql title="Get definition of the table"
SHOW CREATE TABLE DATABASE_NAME.TABLE_NAME\G;
```

```sql title="Rename a table"
RENAME TABLE CURRENT_TABLE_NAME TO NEW_TABLE_NAME;
```

```sql title="Create new table like from exists table"
CREATE TABLE TABLE_NAME LIKE EXISTS_TABLE;

-- create new table (structure keys and indexes are copied over as well, **without data**)
```
