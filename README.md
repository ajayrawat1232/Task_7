# Task_7
## Sales Data Summary and Visualization

## Overview
This project demonstrates how to create, populate, and analyze a simple sales database using SQLite and Python. It includes a script that:

Creates a SQLite database (sales_data.db) with a sales table.
Inserts 8,000 rows of dummy sales data (products, quantities, prices).
Runs SQL queries to summarize total quantity sold and revenue by product.
Prints the summary results.
Visualizes revenue by product using a bar chart saved as sales_chart.png.
This project is ideal for beginners learning database operations, SQL querying, and data visualization with Python.

## Features
Database creation and connection using sqlite3.
Automated dummy data generation with NumPy.
SQL aggregation queries executed via Pandas.
Matplotlib bar chart visualization of sales revenue.
Robust and modular Python code with logging and error handling.
## Requirements
Python 3.6+
Packages:
pandas
matplotlib
numpy
You can install the required packages with:

pip install pandas matplotlib numpy
## Usage
# Clone the repository:

git clone https://github.com/your-username/sales-data-summary.git
cd sales-data-summary
Run the script:

python sales_summary.py
This will:

Create sales_data.db if it doesn't exist.
Insert dummy sales data if the table is empty.
Print the sales summary grouped by product.
Display and save a bar chart (sales_chart.png) showing revenue by product.
Project Structure
sales-data-summary/
│
├── sales_summary.py       # Main Python script with database and visualization logic
├── sales_data.db          # SQLite database file (created after running the script)
├── sales_chart.png        # Generated revenue bar chart image
└── README.md              # This file
## Code Highlights
# Database connection and table creation:

conn = sqlite3.connect("sales_data.db")
cursor.execute("""
    CREATE TABLE IF NOT EXISTS sales (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        product TEXT,
        quantity INTEGER,
        price REAL
    )
""")
Dummy data insertion:

products = ['Product_A', 'Product_B', 'Product_C', 'Product_D', 'Product_E']
rows = [(np.random.choice(products), np.random.randint(1, 20), round(np.random.uniform(5, 100), 2)) for _ in range(8000)]
cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)", rows)
Sales summary query and visualization:

query = """
SELECT product, SUM(quantity) AS total_qty, SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""
df = pd.read_sql_query(query, conn)
df.plot(kind='bar', x='product', y='revenue')
plt.savefig("sales_chart.png")
plt.show()
Happy coding! 🚀

Feel free to customize the repository URL, contact info, or add any badges (like build status or license) as you see fit.
