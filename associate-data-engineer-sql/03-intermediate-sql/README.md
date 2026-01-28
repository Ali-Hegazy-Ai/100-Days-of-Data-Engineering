# Intermediate SQL

## Course Roadmap
- Querying databases
- Count and view records
- Understand query execution and style
- Filtering and aggregate functions
- Sorting and grouping

## COUNT()
Counts the number of records in a field.

## Order of Execution
SQL is not processed in its written order:
1. FROM first
2. Then SELECT
3. Then LIMIT

## Debugging SQL Code
Perhaps you mean...

## SQL Formatting
- Not required but recommended
- Best practices: capitalize keywords and use new lines

---

# Filtering Data

## 1. WHERE Clause – Basics
- **Purpose:** Filters rows based on a condition.
- **Syntax:** `WHERE condition`
- **Example:**  
  ```sql
  SELECT title FROM films WHERE release_year > 1960;
  ```

---

## 2. Comparison Operators
| Operator | Meaning | Example |
|----------|---------|---------|
| `>` | Greater than | `WHERE release_year > 1960` |
| `<` | Less than | `WHERE release_year < 1960` |
| `>=` | Greater than or equal to | `WHERE release_year >= 1960` |
| `<=` | Less than or equal to | `WHERE release_year <= 1960` |
| `=` | Equal to | `WHERE release_year = 1960` |
| `<>` or `!=` | Not equal to | `WHERE release_year <> 1960` |

---

## 3. Filtering Strings
- **Strings must be in single quotes:** `'Japan'`
- **Case-sensitive:** `'Japan'` ≠ `'japan'`
- **Example:**  
  ```sql
  SELECT title FROM films WHERE country = 'Japan';
  ```

---

## 4. Order of Execution
1. **FROM** – Identify the table  
2. **WHERE** – Filter rows  
3. **SELECT** – Choose columns  
4. **LIMIT** – Restrict rows  
- **Example Query:**  
  ```sql
  SELECT item FROM coats WHERE color = 'green' LIMIT 5;
  ```

---

## 5. Multiple Criteria

### OR Operator
- At least one condition must be true.
- **Correct:**  
  ```sql
  WHERE release_year = 1994 OR release_year = 2000
  ```
- **Incorrect:**  
  ```sql
  WHERE release_year = 1994 OR 2000  -- Missing condition
  ```

### AND Operator
- All conditions must be true.
- **Correct:**  
  ```sql
  WHERE release_year > 1994 AND release_year < 2000
  ```
- **Incorrect:**  
  ```sql
  WHERE release_year > 1994 AND < 2000  -- Incomplete condition
  ```

### Combining AND/OR
- Use parentheses to group logic:
  ```sql
  WHERE (release_year = 1994 OR release_year = 1995) 
    AND (certification = 'PG' OR certification = 'R')
  ```

### BETWEEN Operator
- Inclusive range check.
- **Equivalent to:** `release_year >= 1994 AND release_year <= 2000`
- **Example:**  
  ```sql
  WHERE release_year BETWEEN 1994 AND 2000
  ```

---

## 6. Filtering Text with Patterns

### LIKE & NOT LIKE
- `%` – Matches zero, one, or many characters.
- `_` – Matches exactly one character.
- **Examples:**  
  ```sql
  WHERE name LIKE 'Ade%'   -- Starts with "Ade"
  WHERE name LIKE 'Ev_'    -- Three letters, starts with "Ev"
  WHERE name NOT LIKE 'A.%' -- Excludes names starting with "A."
  ```

### IN Operator
- Checks if a value matches any in a list.
- **Examples:**  
  ```sql
  WHERE release_year IN (1920, 1930, 1940)
  WHERE country IN ('Germany', 'France')
  ```

---

## 7. NULL Values
- **NULL** = missing/unknown value.
- **Check for NULL:** `IS NULL`
- **Exclude NULL:** `IS NOT NULL`
- **Examples:**  
  ```sql
  WHERE birthdate IS NULL
  WHERE birthdate IS NOT NULL
  ```

### COUNT() with NULL
- `COUNT(column)` ignores NULLs.
- `COUNT(*)` counts all rows, including NULLs.
- **Example:**  
  ```sql
  SELECT COUNT(certification) FROM films;  -- Ignores NULL certs
  SELECT COUNT(*) FROM films;              -- Counts all rows
  ```

---

## 8. Key Takeaways
- Use **single quotes** for strings.
- **Parentheses** control logical precedence.
- **BETWEEN** is inclusive.
- **LIKE** uses `%` and `_` for patterns.
- **NULL** requires `IS NULL`/`IS NOT NULL`.
- **COUNT(column)** excludes NULLs; **COUNT(*)** includes them.

---

# Summarizing Data

## 1. Aggregate Functions
- **Purpose:** Return a single value from a column or set of rows.
- **Common Functions:**
  - `AVG()` – Average of numeric values
  - `SUM()` – Sum of numeric values
  - `MIN()` – Minimum value (works on numbers, text, dates)
  - `MAX()` – Maximum value (works on numbers, text, dates)
  - `COUNT()` – Count of non-NULL values

- **Examples:**
  ```sql
  SELECT AVG(budget) FROM films;
  SELECT MIN(country) FROM films; -- Returns first alphabetically
  SELECT COUNT(*) FROM films;      -- Counts all rows
  ```

---

## 2. Aggregate Functions with WHERE
- **Filter before aggregating.**
- **Example:**
  ```sql
  SELECT AVG(budget) AS avg_budget 
  FROM films 
  WHERE release_year >= 2010;
  ```

- **Other Examples:**
  ```sql
  SELECT SUM(budget) FROM films WHERE release_year = 2010;
  SELECT MIN(budget) FROM films WHERE release_year = 2010;
  ```

---

## 3. ROUND() Function
- **Rounds a number to specified decimal places.**
- **Syntax:** `ROUND(number, decimal_places)`
- **If decimal_places is:**
  - **Positive:** Rounds to that many decimal places
  - **Zero:** Rounds to whole number
  - **Negative:** Rounds to left of decimal (e.g., -3 rounds to nearest thousand)

- **Examples:**
  ```sql
  SELECT ROUND(AVG(budget), 2) FROM films;  -- Two decimals
  SELECT ROUND(AVG(budget), 0) FROM films;  -- Whole number
  SELECT ROUND(AVG(budget), -5) FROM films; -- Nearest 100,000
  ```

---

## 4. Arithmetic Operators
- **Basic Operators:** `+`, `-`, `*`, `/`
- **Note:** Integer division truncates. Use decimals for precise division.
  ```sql
  SELECT 4 / 3;      -- Returns 1 (integer division)
  SELECT 4.0 / 3.0;  -- Returns 1.333...
  ```
- **Use with Columns:**
  ```sql
  SELECT (gross - budget) AS profit FROM films;
  ```

---

## 5. Aliasing
- **Purpose:** Rename columns in output for clarity.
- **Placement:** Defined in `SELECT` clause.
- **Syntax:** `column_name AS alias_name`
- **Examples:**
  ```sql
  SELECT MIN(country) AS min_country FROM films;
  SELECT MAX(budget) AS max_budget, MAX(duration) AS max_duration FROM films;
  ```

---

## 6. Order of Execution with Aliases
1. **FROM** – Identify table(s)
2. **WHERE** – Filter rows
3. **SELECT** – Choose/calculate columns *(aliases defined here)*
4. **LIMIT** – Restrict output rows

- **Key Rule:** **Aliases cannot be used in WHERE clause** because WHERE executes before SELECT.
  ```sql
  -- ERROR:
  SELECT budget AS max_budget FROM films WHERE max_budget IS NOT NULL;
  
  -- CORRECT:
  SELECT budget AS max_budget FROM films WHERE budget IS NOT NULL;
  ```

---

## 7. Aggregate Functions vs. Arithmetic
| **Aggregate Functions**          | **Arithmetic Operations**          |
|----------------------------------|------------------------------------|
| Operate across multiple rows     | Operate within a single row        |
| Return single summary value      | Return value per row               |
| Examples: `SUM()`, `AVG()`       | Examples: `(gross - budget)`       |
| Used with `GROUP BY` (later)     | Used in column expressions         |

---

## 8. Key Takeaways
- `MIN()`/`MAX()` work on numbers, text, and dates.
- `COUNT(column)` excludes NULLs; `COUNT(*)` includes them.
- Filter with `WHERE` **before** aggregating.
- Use `ROUND()` to format numeric results.
- Aliases improve readability but can't be used in `WHERE`.
- Integer division truncates; use decimals for accuracy.

---

# Sorting & Grouping Data

## 1. Sorting Results (ORDER BY)
- **Purpose:** Arrange query results in ascending (ASC) or descending (DESC) order.
- **Basic syntax:**  
  ```sql
  SELECT column1, column2
  FROM table
  ORDER BY column1 [ASC|DESC];
  ```
- **Example:**
  ```sql
  SELECT title, budget FROM films ORDER BY budget DESC;
  ```
- **Multiple fields:**  
  Use a comma to sort by one column, then another (like a tie-breaker).
  ```sql
  SELECT title, wins, imdb_score
  FROM best_movies
  ORDER BY wins DESC, imdb_score DESC;
  ```
- **Note:** `NULL` values are sorted first in `ASC` order, last in `DESC`. Use `IS NOT NULL` to exclude them.

---

## 2. Grouping Data (GROUP BY)
- **Purpose:** Summarize data by groups (e.g., count, average).
- **Basic syntax:**  
  ```sql
  SELECT column, COUNT(*)
  FROM table
  GROUP BY column;
  ```
- **Example:**
  ```sql
  SELECT certification, COUNT(title) AS title_count
  FROM films
  GROUP BY certification;
  ```
- **⚠️ Rule:** Any column in `SELECT` must be in `GROUP BY` or inside an aggregate function (like `COUNT`, `AVG`).
- **Multiple fields:** Group by more than one column.
  ```sql
  SELECT certification, language, COUNT(title)
  FROM films
  GROUP BY certification, language;
  ```

---

## 3. Sorting Grouped Results
- Combine `GROUP BY` with `ORDER BY`:
  ```sql
  SELECT certification, COUNT(title) AS title_count
  FROM films
  GROUP BY certification
  ORDER BY title_count DESC;
  ```

---

## 4. Filtering Grouped Data (HAVING)
- **Purpose:** Filter groups (after `GROUP BY`), unlike `WHERE` which filters rows before grouping.
- **Syntax:**  
  ```sql
  SELECT column, COUNT(*)
  FROM table
  GROUP BY column
  HAVING COUNT(*) > 10;
  ```
- **Example:** Find years with more than 10 films:
  ```sql
  SELECT release_year, COUNT(title)
  FROM films
  GROUP BY release_year
  HAVING COUNT(title) > 10;
  ```
- **`WHERE` vs `HAVING`:**
  - `WHERE`: Filters individual rows before grouping.
  - `HAVING`: Filters groups after aggregation.

---

## 5. Order of Execution (Key Sequence)
1. `FROM` → 2. `WHERE` → 3. `GROUP BY` → 4. `HAVING` → 5. `SELECT` → 6. `ORDER BY` → 7. `LIMIT`

---

## 6. Skills Covered
- Sorting with `ORDER BY`
- Grouping with `GROUP BY`
- Filtering groups with `HAVING`
- Error handling in grouped queries
- Writing clear, readable SQL

---

# INNER JOIN

## 1. What is INNER JOIN?
INNER JOIN returns only the rows that have matching values in **both** tables.

### Key Principle:
- Looks for records in both tables that match on a specified field
- Non-matching records from either table are **excluded**

### Visual Example:
```
Table A (left)        Table B (right)
id | name            id | city
1  | Alice           1  | Paris
2  | Bob             3  | London
3  | Charlie         4  | Tokyo

INNER JOIN on id:
id | name    | city
1  | Alice   | Paris
3  | Charlie | London
```

---

## 2. Basic INNER JOIN Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

### Example:
```sql
SELECT prime_ministers.country, 
       prime_ministers.continent,
       prime_minister,
       president
FROM presidents
INNER JOIN prime_ministers
ON presidents.country = prime_ministers.country;
```

---

## 3. Table Aliases - Making Queries Cleaner

```sql
SELECT p2.country, 
       p2.continent,
       prime_minister,
       president
FROM presidents AS p1  -- p1 is alias for presidents
INNER JOIN prime_ministers AS p2  -- p2 is alias for prime_ministers
ON p1.country = p2.country;
```

**Why use aliases?**
- Shorter, cleaner code
- Essential when joining the same table multiple times
- Reduces typing errors

---

## 4. USING Clause - Simplified Syntax

When column names are **identical** in both tables:

```sql
SELECT p2.country, p2.continent, prime_minister, president
FROM presidents AS p1
INNER JOIN prime_ministers AS p2
USING(country);  -- Instead of ON p1.country = p2.country
```

**Note:** `USING` only works when column names are exactly the same

---

## 5. Database Relationships & JOIN Applications

### A. One-to-Many Relationship
**Example:** Authors to Books
- One author writes many books
- One book has one author

```sql
SELECT authors.first_name, authors.last_name, books.title
FROM authors
INNER JOIN books
ON authors.author_id = books.author_id;
```

### B. One-to-One Relationship
**Example:** Individuals to Fingerprints
- One person has one fingerprint record
- One fingerprint record belongs to one person

```sql
SELECT individuals.first_name, individuals.last_name
FROM individuals
INNER JOIN fingerprints
ON individuals.passport_no = fingerprints.passport_no;
```

### C. Many-to-Many Relationship
**Example:** Students ↔ Courses
- One student takes many courses
- One course has many students

**Requires a junction table:**
```sql
SELECT students.name, courses.course_name
FROM students
INNER JOIN student_courses ON students.id = student_courses.student_id
INNER JOIN courses ON student_courses.course_id = courses.id;
```

---

## 6. Chaining Multiple JOINs

```sql
SELECT p1.country, p1.continent,
       president, prime_minister, pm_start
FROM prime_ministers as p1
INNER JOIN presidents as p2 USING(country)
INNER JOIN prime_minister_terms as p3 USING(prime_minister);
```

---

## 7. JOINing on Multiple Keys

For more precise matching:

```sql
SELECT *
FROM orders
INNER JOIN shipments
ON orders.order_id = shipments.order_id
AND orders.order_date = shipments.ship_date;
```

---

## 8. Key Takeaways

1. **INNER JOIN = Intersection** of two tables
2. **Always specify** the matching condition with `ON` or `USING`
3. **Use aliases** for cleaner code, especially with multiple joins
4. **Understand relationships** between tables before joining
5. **Chain JOINs** to combine data from multiple tables
6. **Multiple key joins** provide more precise matching

---

*Notes compiled from DataCamp's Intermediate SQL and Joining Data courses*
