```sql
SELECT SYSDATETIME();
SELECT DATENAME(YEAR, '2005-12-31 23:59:59.9999999')
,DATENAME(MONTH, '2005-12-31 23:59:59.9999999')
,DATENAME(DAY, '2005-12-31 23:59:59.9999999')
,DATENAME(DAYOFYEAR, '2005-12-31 23:59:59.9999999')
,DATENAME(WEEKDAY, '2005-12-31 23:59:59.9999999');
SELECT DATEDIFF(YEAR, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(QUARTER, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(MONTH, '2015-01-01 ','2015-12-31 ');
SELECT DATEDIFF(DAYOFYEAR, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(DAY, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(WEEK, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(HOUR, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(MINUTE, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT CONCAT('ronak','sheth');
SELECT CONCAT(RTRIM(' ronak          '),'sheth');
SELECT UPPER('ronak');
SELECT SUBSTRING('ronak',2,3);
SELECT len('ronak');
SELECT ROUND(11.62,2);
SELECT ROUND(114335.624,-2);
SELECT FLOOR(11.79);
SELECT CEILING(11.79);
```