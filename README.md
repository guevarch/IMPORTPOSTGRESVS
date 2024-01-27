# PostgreSQL Data Import Using Python

This repository includes a Python script to import data from CSV files into a PostgreSQL database. The script uses `psycopg2` to connect to the PostgreSQL instance and perform SQL operations.

## Database Connection

First, we setup the connection to the PostgreSQL database.

```python
import psycopg2

# Connect to the PostgreSQL database
conn = psycopg2.connect(database="postgres",
                        user='postgres', password='postgres',
                        host='127.0.0.1', port='5432'
)
```

## Titles Table Import

Next, we read data from `titles.csv` and insert it into the `titles` table.

```python
cur = conn.cursor()

with open('titles.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)  # Skip the header row.
    for row in reader:
        title_id = (row[0])
        title = row[1]
        cur.execute(
            "INSERT INTO titles (title_id, title) VALUES (%s, %s)",
            (title_id, title)
        )

conn.commit()
```

## Employees Table Import

We also process `employees.csv`, format date columns, and insert the data into the `employees` table.

```python
cur = conn.cursor()

with open('employees.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)  # Skip the header row.
    for row in reader:
        ... # Processing of employee data with datetime parsing omitted for brevity

conn.commit()
```

## Additional Tables

Similar patterns are followed for importing data into other tables such as `departments`, `dept_manager`, `dept_emp`, and `salaries`.

```python
# Code for other imports is similar: opening cursor, reading from CSV, INSERT into table...
```

After finishing the import for each table, a commit operation is performed to ensure the data is saved in the database.

## Closing Connections

Finally, after all data imports are done, we close the cursor and the database connection.

```python
cur.close()
conn.close()
```

Ensure that you replace database credentials with your actual credentials and that the CSV files are properly formatted and available in the local directory from which the script is being run.

## Requirements

- Python 3
- psycopg2 module
- A running PostgreSQL server

To install the required modules, run:

```shell
pip install psycopg2
```

Please adjust the CSV file paths and database details according to your local environment before running the script.
