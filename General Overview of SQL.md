## First, lets talk basics! 

*SELECT* : 
All SQL code will **ALWAYS** have SELECT AND FROM. For example:
```sql
SELCT
column1, #remeber to separate columns by ','
column2,
function calculation (such as CONCAT, SUM, AVG, etc.) #functions and concatination can also happen in this section
FROM table1;
```
In general, when you want to view all the columns in a table, use '*[star *]*'. For example: 
```sql 
SELECT * FROM table1; #be mindful when using the star
```
When we dont want to select all the columns, but only show 2 columns. We can explicitly tell SQL which columns we want to return. For example:
```sql
SELCT
column1 [column name],
column2 [column name],
FROM table1;
```

*LIMITING* :

Limit is used when we want to 'limit' how many rows we want to return in our SQL session. This is important when we are using data we have never seen before, and want to see only the top 10 or top 20 records. Recommendation: Apply *limit* using a number, this lets SQL know how many rows we want from the query. *Limit* is equivalent to *top* or *head*. For example: 
```sql 
SELECT * FROM table1
LIMIT 10; 
```

*SORTING*: Very intuitive when it comes with SQL, why do we want to sort? 

Lets get the first 5 values in column1 from table1 by alphabetical order:
```sql
SELECT column1
FROM table1
ORDER BY column1  #sort by using ORDER BY, default to alphabetical order. Or you can use ASC argument for ascending, and DESC for descending. Order by is always after the FROM
LIMIT 5; 
```


