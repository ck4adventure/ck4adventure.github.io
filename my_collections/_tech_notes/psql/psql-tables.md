## PSQL Tables pt 1

from the intro we learned that tables can be created and dropped, and that they are a virtual representation of rows and columns drawn on a piece of paper

each col must have a name and a data type
a row is an entry of data that contains a value for every column

there must be a value for every column, by default it's null

it can be set to a value, or even to an expression, 
as is done for timestamps to get now,
and for ids either incrementing or unique

shorthand for assigning the next incrementing value - `SERIAL`

### Generated Columns
direct from docs:
A generated column is a special column that is always computed from other columns. Thus, it is for columns what a view is for tables. There are two kinds of generated columns: stored and virtual. A stored generated column is computed when it is written (inserted or updated) and occupies storage as if it were a normal column. A virtual generated column occupies no storage and is computed when it is read. Thus, a virtual generated column is similar to a view and a stored generated column is similar to a materialized view (except that it is always updated automatically). PostgreSQL currently implements only stored generated columns.

To create a generated column, use the GENERATED ALWAYS AS clause in CREATE TABLE, for example:

```sql
CREATE TABLE people (
    ...,
    height_cm numeric,
    height_in numeric GENERATED ALWAYS AS (height_cm / 2.54) STORED
);
```

There are a few rules, such as generated columns can't reference other generated columns, and that their values are not directly modifiable, but most are common sense.

### Data Constraints
One of the more important things in a db is ensuring the right type of data is stored for each column. Setting the basic data type is just the beginning.
- check constraints
- non-null constraints
- unique constaints
- primary key constraints
- foreign key constraints
- exclusion constraints

#### Check Constraints
can be on the column directly, like price > 0
or, can be for the table, keyword is `CHECK` plus conditionals that evaluate to a bool

```sql
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0),
    discounted_price numeric,
    CHECK (discounted_price > 0 AND price > discounted_price)
);
```

The CONSTRAINT keyword is a way to specify a name for it
```sql
CONSTRAINT valid_discount CHECK (price > discounted_price)
```

NOTE: if any of the values are null, the check constraint will not prevent this and still be satisfied. But, there is a not null constraint.

#### Not null constraint
By default pgsql will allow null values for any given column. Specifying NULL will also get this behavior, although rarely useful to be stated explicitly. 
Stating `NOT NULL` will create a constraint that a value must be present in order for any create/update operation to be successful.

In practice, the majority of columns will end up marked not null.

#### Unique Constraints
Unique constraints ensure that the data contained in a column, or a group of columns, is unique among all the rows in the table. They can also be named in the same way as other constraints. Adding a unique constraint will automatically create a unique B-tree index on the column or group of columns listed in the constraint.

```sql
CREATE TABLE products (
    product_no integer CONSTRAINT must_be_different UNIQUE,
    name text,
    price numeric
);
```
when written as a column constraint, and:

```sql
CREATE TABLE products (
    product_no integer CONSTRAINT must_be_different UNIQUE,
    name text,
    price numeric,
    UNIQUE (product_no)
);
```
when written as a table constraint.

Unique combinations are declared this way (def same but not same as rails)
```sql
CREATE TABLE example (
    a integer,
    b integer,
    c integer,
    UNIQUE (a, c)
);
```

In general, a unique constraint is violated if there is more than one row in the table where the values of all of the columns included in the constraint are equal. By default, two null values are not considered equal in this comparison. That means even in the presence of a unique constraint it is possible to store duplicate rows that contain a null value in at least one of the constrained columns. This behavior can be changed by adding the clause NULLS NOT DISTINCT, like

```sql
CREATE TABLE products (
    product_no integer UNIQUE NULLS NOT DISTINCT,
    name text,
    price numeric
);
```

#### Primary Keys as Constraints
A primary key constraint indicates that a column, or group of columns, can be used as a unique identifier for rows in the table. This requires that the values be both unique and not null. So, the following two table definitions accept the same data:

```sql
CREATE TABLE products (
    product_no integer UNIQUE NOT NULL,
    name text,
    price numeric
);
```
```sql
CREATE TABLE products (
    product_no integer PRIMARY KEY,
    name text,
    price numeric
);
```

Adding a primary key will automatically create a unique B-tree index on the column or group of columns listed in the primary key, and will force the column(s) to be marked NOT NULL.

A table can have at most one primary key. (There can be any number of unique and not-null constraints, which are functionally almost the same thing, but only one can be identified as the primary key.) 

### Foreign Keys
A very handy use case for maintaining unique identifiers as primary keys is that they can be referenced as foreign keys on other tables. Foreign keys reference values in another table, most often using the primary key of the other table for lookup, but that isn't mandatory if there is another unique column. Here, `(product_no)` is optional since pg will default to the pk of the referenced table.

```sql
CREATE TABLE orders (
    order_id integer PRIMARY KEY,
    product_no integer REFERENCES products (product_no),
    quantity integer
);
```

Sometimes it is useful for the “other table” of a foreign key constraint to be the same table; this is called a self-referential foreign key. For example, if you want rows of a table to represent nodes of a tree structure, you could write

```sql
CREATE TABLE tree (
    node_id integer PRIMARY KEY,
    parent_id integer REFERENCES tree,
    name text,
    ...
);
```

#### Many to Many Relationships
To illustrate this, let's implement the following policy on the many-to-many relationship example above: when someone wants to remove a product that is still referenced by an order (via order_items), we disallow it. If someone removes an order, the order items are removed as well. Note the different types of ON DELETE actions used. `RESTRICT` prevents deletion of the referenced object and `CASCADE` ensures it. There is also `NO ACTION` which will error later if the referenced object isn't handled.

My aha moment is the the actions are asking what to do with that entry if the referenced entry is deleted or updated.

```sql
CREATE TABLE products (
    product_no integer PRIMARY KEY,
    name text,
    price numeric
);

CREATE TABLE orders (
    order_id integer PRIMARY KEY,
    shipping_address text,
    ...
);

CREATE TABLE order_items (
    product_no integer REFERENCES products ON DELETE RESTRICT,
    order_id integer REFERENCES orders ON DELETE CASCADE,
    quantity integer,
    PRIMARY KEY (product_no, order_id)
);
```

The actions SET NULL and SET DEFAULT can take a column list to specify which columns to set. Normally, all columns of the foreign-key constraint are set; setting only a subset is useful in some special cases. Consider the following example:

```sql
CREATE TABLE tenants (
    tenant_id integer PRIMARY KEY
);

CREATE TABLE users (
    tenant_id integer REFERENCES tenants ON DELETE CASCADE,
    user_id integer NOT NULL,
    PRIMARY KEY (tenant_id, user_id)
);

CREATE TABLE posts (
    tenant_id integer REFERENCES tenants ON DELETE CASCADE,
    post_id integer NOT NULL,
    author_id integer,
    PRIMARY KEY (tenant_id, post_id),
    FOREIGN KEY (tenant_id, author_id) REFERENCES users ON DELETE SET NULL (author_id)
);
```

### Exclusion Constraints
5.4.6. Exclusion Constraints 
Exclusion constraints ensure that if any two rows are compared on the specified columns or expressions using the specified operators, at least one of these operator comparisons will return false or null. The syntax is:

CREATE TABLE circles (
    c circle,
    EXCLUDE USING gist (c WITH &&)
);