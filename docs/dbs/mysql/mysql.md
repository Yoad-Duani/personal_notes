# Mysql

Add  and update recoreds

```sql title="add"
INSERT INTO DB_NAME.TABLE_NAME (column1, column2) VALUES(value1, value2)
```

```sql title="update"
UPDATE DB_NAME.TABLE_NAME set column1=value1 WHERE column2=some_value
```

Table size

```sql
SELECT
    table_name AS `Table`,
    round(((data_length + index_length) / 1024 / 1024), 2) `Size in MB`
FROM information_schema.TABLES
WHERE table_schema = "<DATABASE>"
    AND table_name = "<Table>";
-- (1)!
```

1. Shows the table size in MB, it is possible to add more /1024 to show in GB, replace `DATABASE` and `Table`

mysqldumb

```bash
mysqldump -h <MYSQL_HOST>--port <PORT> --user=<USERNAME> --password=<PASSWORD> --skip-column-statistics <DB_NAME> > <DUNMP_FILE>
#for example:
mysqldump -h 127.0.0.1 --port 33061 --user=... --password=... --skip-column-statistics son > mysql.dump
```

mysql restore

```bash
mysql -h 127.0.0.1 -u <USERNAME> -p<PASSWORD> < FILE_NAME.dump
```

Actions on table

```sql
-- Definition of the table ()
SHOW CREATE TABLE <Table_name>\G;
 
-- rename table
RENAME TABLE <current_name> TO <new_name>;
 
-- create new table (structure keys and indexes are copied over as well, *without data*)
CREATE TABLE <new_table> LIKE <exist_table>;
```
