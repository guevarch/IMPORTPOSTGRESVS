# IMPORTPOSTGRESVS

import psycopg2
import csv

# Connect to the PostgreSQL database
conn = psycopg2.connect(database="postgres",
						user='postgres', password='postgres',
						host='127.0.0.1', port='5432'
)

# Open a cursor to perform database operations
cur = conn.cursor()

# Read the data from the CSV file and insert it into the database
with open('FILE.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader) # Skip the header row.
    for row in reader:
        title_id = (row[0])
        title = row[1]
        cur.execute(
            "INSERT INTO titles (COL1, COL2) VALUES (%s, %s)",
            (COL1, COL2)
        )
## (%s, %s) WILL CHANGE BASED ON HOW MANY COLS
# Commit the transaction and close the cursor and connection
conn.commit()
cur.close()
conn.close()
