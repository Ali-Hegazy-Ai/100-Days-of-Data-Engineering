# Introduction to SQL

## Course Goals
- Understand databases and their structure
- Extract information from databases using SQL

## Structured Query Language (SQL)

### Tables

**Table Naming Best Practices:**
- Clear
- Refer to the data
- Lowercase
- Use underscores

### Data Types
Different columns store different types of data.

## SQL Keywords

### SELECT Statement
```sql
SELECT "name" FROM table_name

SELECT name 
FROM patrons;
```

The `*` selects all columns.

### Aliasing with AS
```sql
SELECT name AS n
FROM employee
```

## SQL Flavors
They have an ISO standard but different database systems have different extras.

### Types:
- **PostgreSQL**
  - Free
  - Open source
  - Name of the database and SQL flavor
  
- **SQL Server**
  - Free and paid versions
  - Created by Microsoft
  - T-SQL flavor

### Example Differences
In PostgreSQL: `LIMIT`
In SQL Server: `TOP`

---

*Notes compiled from DataCamp's Introduction to SQL course*
