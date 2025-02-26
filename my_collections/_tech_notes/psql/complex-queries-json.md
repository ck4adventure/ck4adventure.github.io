---
layout: page
title: Building JSON in Queries
topic: pgsql
---
Here are a few helpful things that I learned while working on my recipe app.

## JSON_BUILD_OBJECT
Creates a json object. `JSON_BUILD_OBJECT(key1, value1, key2, value2, ...)`


## JSON_AGG
This function aggregates multiple JSON objects into an array.

Example:
`SELECT JSON_AGG(JSON_BUILD_OBJECT('ingredient', name, 'quantity', qty)) 
FROM recipe_ingredients;`

```sql
[
  {"ingredient": "Flour", "quantity": 2},
  {"ingredient": "Milk", "quantity": 1}
]
```



## TO_JSON
This function converts a PostgreSQL row or value into JSON format.

Example:
`SELECT TO_JSON(ROW('Pancakes', 'Mix, Cook, Serve'));`

```sql
{"f1": "Pancakes", "f2": "Mix, Cook, Serve"}
```


## JSON_OBJ_AGG
This function aggregates rows into a JSON object where one column is the key and another is the value.
Example:
`SELECT JSON_OBJECT_AGG(name, steps) FROM recipes;`

```json
{
  "Pancakes": "Mix, Cook, Serve",
  "Omelette": "Whisk, Cook, Flip"
}
```