
---
![[Pasted image 20260128231014.png]]
## INNER JOIN

### What it does

- Returns **only rows that match in both tables**.
    
- If a value does not exist in one table, it is removed from the result.
    

### Mental model

- Think of it as the **overlap** between two tables.
    

### Diagram idea

- Only the middle part where both tables match.
    

### Syntax

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id;
```

### Key points

- Most strict join.
    
- No `NULL` values caused by missing matches.
    
- Used when data **must exist in both tables**.
    

---

## LEFT JOIN (LEFT OUTER JOIN)

### What it does

- Returns **all rows from the left table**.
    
- Adds matching rows from the right table.
    
- If no match is found, right table columns become `NULL`.
    

### Mental model

- “Keep everything from the left table.”
    

### Why it is useful

- When you want a **complete list** from one table.
    
- Missing related data should still appear.
    

### Syntax

```sql
SELECT *
FROM left_table
LEFT JOIN right_table
ON left_table.id = right_table.id;
```

### Example

```sql
SELECT p1.country, prime_minister, president
FROM prime_ministers AS p1
LEFT JOIN presidents AS p2
USING (country);
```

### Example result explanation

- Countries without presidents still appear.
    
- Their `president` value is `NULL`.
    

### Important notes

- `LEFT JOIN` = `LEFT OUTER JOIN`
    
- Rows that exist **only** in the right table are ignored.
    

---

## RIGHT JOIN (RIGHT OUTER JOIN)

### What it does

- Returns **all rows from the right table**.
    
- Adds matching rows from the left table.
    
- If no match is found, left table columns become `NULL`.
    

### Mental model

- “Keep everything from the right table.”
    

### Syntax

```sql
SELECT *
FROM left_table
RIGHT JOIN right_table
ON left_table.id = right_table.id;
```

### Example

```sql
SELECT p1.country, prime_minister, president
FROM prime_ministers AS p1
RIGHT JOIN presidents AS p2
USING (country);
```

### Why RIGHT JOIN is rare

- Any RIGHT JOIN can be rewritten as a LEFT JOIN.
    
- LEFT JOIN is easier to read and write.
    
- SQL is read left to right.
    

### Rule to remember

> Prefer LEFT JOIN.  
> Use RIGHT JOIN only if required.

---

## FULL JOIN (FULL OUTER JOIN)

### What it does

- Returns **all rows from both tables**.
    
- Matches rows where possible.
    
- Uses `NULL` when there is no match.
    

### Mental model

- LEFT JOIN + RIGHT JOIN combined.
    

### Syntax

```sql
SELECT *
FROM table1
FULL JOIN table2
ON table1.id = table2.id;
```

### Example

```sql
SELECT p1.country, prime_minister, president
FROM prime_ministers AS p1
FULL JOIN presidents AS p2
ON p1.country = p2.country
LIMIT 10;
```

### Result behavior

- Countries with only a prime minister appear.
    
- Countries with only a president appear.
    
- Countries with both appear normally.
    

### Important notes

- `FULL JOIN` = `FULL OUTER JOIN`
    
- Not supported in some databases (example: MySQL).
    

---

## CROSS JOIN

### What it does

- Creates **every possible combination** of rows.
    
- No matching condition is required.
    

### Mental model

- Cartesian product.
    
- If table A has 3 rows and table B has 4 rows, result has 12 rows.
    

### Syntax

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

### Example

```sql
SELECT prime_minister, president
FROM prime_ministers AS p1
CROSS JOIN presidents AS p2
WHERE p1.continent = 'Asia'
  AND p2.continent = 'South America';
```

### When to use

- Generating combinations.
    
- Simulations.
    
- Testing relationships.
    

### Warning

- Can create **very large results**.
    
- Always filter when possible.
    

---

## Self JOIN

### What it does

- A table is joined with **itself**.
    
- Uses aliases to treat it as two tables.
    

### Why use it

- Compare rows inside the same table.
    
- Find relationships within the data.
    

### Example: same continent

```sql
SELECT
  p1.country AS country1,
  p2.country AS country2,
  p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent;
```

### Remove duplicates and self-matches

```sql
SELECT
  p1.country AS country1,
  p2.country AS country2,
  p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent
AND p1.country <> p2.country;
```

### Key notes

- Aliases (`p1`, `p2`) are required.
    
- Common in hierarchical and comparison queries.
    

---

## JOIN comparison table

|Join type|Keeps left|Keeps right|NULLs possible|
|---|---|---|---|
|INNER|No|No|No|
|LEFT|Yes|No|Yes|
|RIGHT|No|Yes|Yes|
|FULL|Yes|Yes|Yes|
|CROSS|All combos|All combos|No (unless data has NULLs)|

---

## Practical rules to remember

- Use `INNER JOIN` when data must exist in both tables.
    
- Use `LEFT JOIN` when missing data is allowed.
    
- Avoid `RIGHT JOIN` unless needed.
    
- Use `FULL JOIN` to see **everything**.
    
- Be careful with `CROSS JOIN`.
    
- Use self joins to compare rows in the same table.
    

---

If you want, next I can:

- Add **visual ASCII diagrams** for Obsidian
    
- Create **exam-style summaries**
    
- Add **common interview questions + answers**