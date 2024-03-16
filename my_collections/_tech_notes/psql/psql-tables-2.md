## PSQL Tables pt 2

### Updating Tables - From the docs
All these actions are performed using the ALTER TABLE command, whose reference page contains details beyond those given here.

5.6.1. Adding a Column 
To add a column, use a command like:

```sql
ALTER TABLE products ADD COLUMN description text;
```

The new column is initially filled with whatever default value is given (null if you don't specify a DEFAULT clause).

	Tip: From PostgreSQL 11, adding a column with a constant default value no longer means that each row of the table needs to be updated when the ALTER TABLE statement is executed. Instead, the default value will be returned the next time the row is accessed, and applied when the table is rewritten, making the ALTER TABLE very fast even on large tables.

However, if the default value is volatile (e.g., clock_timestamp()) each row will need to be updated with the value calculated at the time ALTER TABLE is executed. To avoid a potentially lengthy update operation, particularly if you intend to fill the column with mostly nondefault values anyway, it may be preferable to add the column with no default, insert the correct values using UPDATE, and then add any desired default as described below.

You can also define constraints on the column at the same time, using the usual syntax:

```sql
ALTER TABLE products ADD COLUMN description text CHECK (description <> '');
```
In fact all the options that can be applied to a column description in CREATE TABLE can be used here. Keep in mind however that the default value must satisfy the given constraints, or the ADD will fail. Alternatively, you can add constraints later (see below) after you've filled in the new column correctly.

5.6.2. Removing a Column 
To remove a column, use a command like:
```sql
ALTER TABLE products DROP COLUMN description;
```
Whatever data was in the column disappears. Table constraints involving the column are dropped, too. However, if the column is referenced by a foreign key constraint of another table, PostgreSQL will not silently drop that constraint. You can authorize dropping everything that depends on the column by adding CASCADE:
```sql
ALTER TABLE products DROP COLUMN description CASCADE;
```
See Section 5.14 for a description of the general mechanism behind this.

5.6.3. Adding a Constraint 
To add a constraint, the table constraint syntax is used. For example:
```sql
ALTER TABLE products ADD CHECK (name <> '');
ALTER TABLE products ADD CONSTRAINT some_name UNIQUE (product_no);
ALTER TABLE products ADD FOREIGN KEY (product_group_id) REFERENCES product_groups;
```
To add a not-null constraint, which cannot be written as a table constraint, use this syntax:
```sql
ALTER TABLE products ALTER COLUMN product_no SET NOT NULL;
```
The constraint will be checked immediately, so the table data must satisfy the constraint before it can be added.

5.6.4. Removing a Constraint 
To remove a constraint you need to know its name. If you gave it a name then that's easy. Otherwise the system assigned a generated name, which you need to find out. The psql command \d tablename can be helpful here; other interfaces might also provide a way to inspect table details. Then the command is:
```sql
ALTER TABLE products DROP CONSTRAINT some_name;
```
(If you are dealing with a generated constraint name like $2, don't forget that you'll need to double-quote it to make it a valid identifier.)

As with dropping a column, you need to add CASCADE if you want to drop a constraint that something else depends on. An example is that a foreign key constraint depends on a unique or primary key constraint on the referenced column(s).

This works the same for all constraint types except not-null constraints. To drop a not null constraint use:
```sql
ALTER TABLE products ALTER COLUMN product_no DROP NOT NULL;
```
(Recall that not-null constraints do not have names.)

5.6.5. Changing a Column's Default Value 
To set a new default for a column, use a command like:
```sql
ALTER TABLE products ALTER COLUMN price SET DEFAULT 7.77;
```
Note that this doesn't affect any existing rows in the table, it just changes the default for future INSERT commands.

To remove any default value, use:
```sql
ALTER TABLE products ALTER COLUMN price DROP DEFAULT;
```
This is effectively the same as setting the default to null. As a consequence, it is not an error to drop a default where one hadn't been defined, because the default is implicitly the null value.

5.6.6. Changing a Column's Data Type 
To convert a column to a different data type, use a command like:
```sql
ALTER TABLE products ALTER COLUMN price TYPE numeric(10,2);
```
This will succeed only if each existing entry in the column can be converted to the new type by an implicit cast. If a more complex conversion is needed, you can add a USING clause that specifies how to compute the new values from the old.

PostgreSQL will attempt to convert the column's default value (if any) to the new type, as well as any constraints that involve the column. But these conversions might fail, or might produce surprising results. It's often best to drop any constraints on the column before altering its type, and then add back suitably modified constraints afterwards.

5.6.7. Renaming a Column 
To rename a column:
```sql
ALTER TABLE products RENAME COLUMN product_no TO product_number;
```

5.6.8. Renaming a Table 
To rename a table:
```sql
ALTER TABLE products RENAME TO items;
```

### DB Roles and Privileges
5.7 privs
pg seems to have a RBAC set of controls ready to use. users, groups, and roles are all possible

an owner can make themselves readonly, but they still have the grant option to set themselves otherwise

### DB Row Security
summarized - row level security is crucial for keeping user info secret, and other users from reading/writing things they shouldn't, but still allowing for admins to get in and fix things as needed, as well as perform complete backups
This is actually super relevant and I hope to someday get to do this level of work in production
[Row Level Security](https://www.postgresql.org/docs/current/ddl-rowsecurity.html)

### Schemas
A database contains one or more named schemas, which in turn contain tables. Schemas also contain other kinds of named objects, including data types, functions, and operators. 

All tables are created within the `public` schema by default.

PG has a lot of internal schemas, all prefaced with `pg_`

### Inheritance
pg supports inheritance, with the example of two tables, one that holds cities, with name, elev, etc. And a second that inherits cities, but includes an addtl row of which state it's the capital of. 

    I am still working this out in my head. I suppose it is cleaner to break data like that into two tables when one set is likely operated on differently. But it is so trivial I am having a hard time seeing the value of inherited table definitions.

### Partitioning
Usually this doesn't need to happen until the db exceeds physical memory of the server. Table data can be split into partitions, which can be managed separately.

- Range: The table is partitioned into “ranges” defined by a key column or set of columns, with no overlap between the ranges of values assigned to different partitions
- List: The table is partitioned by explicitly listing which key value(s) appear in each partition.
- Hash: he table is partitioned by specifying a modulus and a remainder for each partition. Each partition will hold the rows for which the hash value of the partition key divided by the specified modulus will produce the specified remainder.


#### Declarative Partitioning
This is the standard way.
PostgreSQL allows you to declare that a table is divided into partitions. The table that is divided is referred to as a partitioned table. The declaration includes the partitioning method as described above, plus a list of columns or expressions to be used as the partition key. 

The partitioned table itself is a “virtual” table having no storage of its own. Instead, the storage belongs to partitions, which are otherwise-ordinary tables associated with the partitioned table. Each partition stores a subset of the data as defined by its partition bounds. All rows inserted into a partitioned table will be routed to the appropriate one of the partitions based on the values of the partition key column(s). Updating the partition key of a row will cause it to be moved into a different partition if it no longer satisfies the partition bounds of its original partition.

To use declarative partitioning in this case, use the following steps:

Create the measurement table as a partitioned table by specifying the PARTITION BY clause, which includes the partitioning method (RANGE in this case) and the list of column(s) to use as the partition key.

```sql
CREATE TABLE measurement (
    city_id         int not null,
    logdate         date not null,
    peaktemp        int,
    unitsales       int
) PARTITION BY RANGE (logdate);
```

Create partitions. Each partition's definition must specify bounds that correspond to the partitioning method and partition key of the parent. Note that specifying bounds such that the new partition's values would overlap with those in one or more existing partitions will cause an error.

Partitions thus created are in every way normal PostgreSQL tables (or, possibly, foreign tables). It is possible to specify a tablespace and storage parameters for each partition separately.

For our example, each partition should hold one month's worth of data, to match the requirement of deleting one month's data at a time. So the commands might look like:
```sql
CREATE TABLE measurement_y2006m02 PARTITION OF measurement
    FOR VALUES FROM ('2006-02-01') TO ('2006-03-01');

CREATE TABLE measurement_y2006m03 PARTITION OF measurement
    FOR VALUES FROM ('2006-03-01') TO ('2006-04-01');

...
CREATE TABLE measurement_y2007m11 PARTITION OF measurement
    FOR VALUES FROM ('2007-11-01') TO ('2007-12-01');

CREATE TABLE measurement_y2007m12 PARTITION OF measurement
    FOR VALUES FROM ('2007-12-01') TO ('2008-01-01')
    TABLESPACE fasttablespace;

CREATE TABLE measurement_y2008m01 PARTITION OF measurement
    FOR VALUES FROM ('2008-01-01') TO ('2008-02-01')
    WITH (parallel_workers = 4)
    TABLESPACE fasttablespace;
```
(Recall that adjacent partitions can share a bound value, since range upper bounds are treated as exclusive bounds.)

If you wish to implement sub-partitioning, again specify the PARTITION BY clause in the commands used to create individual partitions, for example:

```sql
CREATE TABLE measurement_y2006m02 PARTITION OF measurement
    FOR VALUES FROM ('2006-02-01') TO ('2006-03-01')
    PARTITION BY RANGE (peaktemp);
```

After creating partitions of measurement_y2006m02, any data inserted into measurement that is mapped to measurement_y2006m02 (or data that is directly inserted into measurement_y2006m02, which is allowed provided its partition constraint is satisfied) will be further redirected to one of its partitions based on the peaktemp column. The partition key specified may overlap with the parent's partition key, although care should be taken when specifying the bounds of a sub-partition such that the set of data it accepts constitutes a subset of what the partition's own bounds allow; the system does not try to check whether that's really the case.

Inserting data into the parent table that does not map to one of the existing partitions will cause an error; an appropriate partition must be added manually.

It is not necessary to manually create table constraints describing the partition boundary conditions for partitions. Such constraints will be created automatically.

Create an index on the key column(s), as well as any other indexes you might want, on the partitioned table. (The key index is not strictly necessary, but in most scenarios it is helpful.) This automatically creates a matching index on each partition, and any partitions you create or attach later will also have such an index. An index or unique constraint declared on a partitioned table is “virtual” in the same way that the partitioned table is: the actual data is in child indexes on the individual partition tables.

```sql
CREATE INDEX ON measurement (logdate);
```

Ensure that the enable_partition_pruning configuration parameter is not disabled in postgresql.conf. If it is, queries will not be optimized as desired.

#### Maintaining Partitions
They aren't meant to remain static. 

- they can be dropped if the data is old and no longer needed (like logs)
- they can be turned into independent tables that standalone


#### Table Inheritence as Partitioning
just creates the tables differently, more user controlled

also has maint procedures like declarative does

### Foreign Data
it's possible to define tables that are in place (virtually?), data can be fetched from a remote site and stored in memory according to that schema and queried, but data is not persisted.

### 5.13. Other Database Objects 
Tables are the central objects in a relational database structure, because they hold your data. But they are not the only objects that exist in a database. Many other kinds of objects can be created to make the use and management of the data more efficient or convenient. They are not discussed in this chapter, but we give you a list here so that you are aware of what is possible:

- Views
- Functions, procedures, and operators
- Data types and domains
- Triggers and rewrite rules

### Dependency Tracking
pg helps to ensure depencies aren't wiped out on accident

```sql
DROP TABLE products;

ERROR:  cannot drop table products because other objects depend on it
DETAIL:  constraint orders_product_no_fkey on table orders depends on table products
HINT:  Use DROP ... CASCADE to drop the dependent objects too.
```

	According to the SQL standard, specifying either RESTRICT or CASCADE is required in a DROP command. No database system actually enforces that rule, but whether the default behavior is RESTRICT or CASCADE varies across systems.