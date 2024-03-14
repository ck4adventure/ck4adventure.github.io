## PostgreSQL

### DB Level
- `createdb <name>`
- `dropdb <name>`
- access what you created `psql <name>`

### Once in `psql`
Some basics:
- `SELECT version();`
- `SELECT current_date;` 

The psql program has a number of internal commands that are not SQL commands. They begin with the backslash character, “\”. For example, you can get help on the syntax of various PostgreSQL SQL commands by typing:
- `mydb=> \h`


Once done:	
- `mydb=> \q`

### Basic Table Commands
Generally, these are written into scripts/files, but can also be executed from the interactive command line.

To create a table and define all of it's cols, types, and restrictions:

```sql
	CREATE TABLE cities (
			name            varchar(80),
			location        point
	);
```

To drop a table:
```sql
DROP TABLE tablename;
```

And to copy in some data:
```sql
COPY weather FROM '/home/user/weather.txt';
```

Inserting data:
```sql
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');
```

### Query Commands
One of the most simple queries:
```sql
SELECT * FROM weather;
```

But usually it will look more like this:
```sql
SELECT city, temp_lo, temp_hi, prcp, date 
FROM weather;
```

Expressions are allowed in statements as well:
```sql
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date 
FROM weather;
```

Relabeling table names for less typing is super helpul:
```sql
SELECT *
FROM weather w JOIN cities c ON w.city = c.name;
```

A query can be “qualified” by adding a WHERE clause that specifies which rows are wanted. The WHERE clause contains a Boolean (truth value) expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (AND, OR, and NOT) are allowed in the qualification. For example, the following retrieves the weather of San Francisco on rainy days:
```sql
SELECT * 
FROM weather
WHERE city = 'San Francisco' AND prcp > 0.0;
```

And there's order by:
```sql
SELECT * 
FROM weather
ORDER BY city, temp_lo;
```

Getting a list of distinct values is sometimes handy:
```sql
SELECT DISTINCT city
FROM weather;
```

And finally, we can order our distinct list:
```sql
SELECT DISTINCT city
FROM weather
ORDER BY city;
```
