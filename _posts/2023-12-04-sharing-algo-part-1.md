---
layout: post
title: Sharing Algo
category: dev
---

An initially frustrating yet ultimately satisying task given to me at a job was to take a query specification that worked for one part of the product, and create a sharing algorithm that could parse that same specification but use it in a different way to query a separate part of the product. For acceptance criteria I was given a confluence page with a couple examples of queries, and an output definition with the sole requirement of returning a list of unique IDs. On the surface, it sounds trivial, but first you, dear reader, need a bit more context on the data and how the specifications worked.


#### Data
The shape of the data itself wasn't super complex. It can be easily translated into a domain logic of flower blossoms. 

Properties and restrictions
- `size`, based on size_in_cm (string enum): xs, sm,md, lg, xl
- `color` (string enum): red, orange, yellow, green, blue, purple, black, white, pink; formatted as "color" or "color/color" with max 2 colors for multicolored flowers
- `has_thorns` (boolean): true/false

So a flower entry would be something like

```js
id: 1
size: xs
color: "red/orange"
has_thorns: false
```

And a table of data might start to look like so:

| id | size | color | has_thorns |
|---|---|---|---|
| 1 | md | "red" | false |
| 2 | lg | "orange"  | true  |
| 3 | xs | "red/orange"  | false  |
| 4 | sm | "blue" | false |
| 5 | sm | "purple"  | false  |
| 6 | xs | "blue"  | false  |


#### Lists and Ranges
The random resolver tool used normally


How I put the query together the first time



This additional requirement of uniqueness was a challenge because 



Originally, the sharing algo was a query submitted as a json object to a backend server. The query itself was an array of objects, each object having a property called `percentage`, so that a distribution could be created of N1% results with X characteristics and N2% of results with Y characteristics.



evaluated it and returned a json response with the IDs and metadata of the selected items. My first attempt was to parse the query into the ideal final buckets counts.

database of items that have at least 3 queryable properties

### Original
Humans
age ranges 18-25, 26-34, 35-44, 45-54, 55+
sex m/f
eth 6 options

### New
Flowers!
size: xs, sm, md,lg, xl
color: red orange yellow green blue purple black white pink
hasThorns: true/false

so a flower entry would be something like
id: 1
size: xs
color: "red/orange"
hasThorns: false


create 10k entries using a randomizer
then recreate the sharing algo
then create an analyzer

