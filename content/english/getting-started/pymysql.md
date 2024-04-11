---
title: PyMySQL
description: A comprehensive guide on how to work with PyMySQL, a Python library to connect to the MySQL databases.
tags: [PyMySQL, SQL, MySQL]
categories: [Tutorial, Getting Started, Database Connection, Python Package]
image: "/images/getting-started/pymysql.png"
date: 2024-01-13
author:
  title: Ayush Jain
  twitter: AyushGanna
---

## Introduction

[MySQL](https://www.mysql.com/){:target="_blank"}is an open-source database system that uses SQL (Structured Query Language) for managing data. It's popular for both small and large projects.

PyMySQL is a Python library for connecting to a MySQL database. It's written in Python, easy to use, and works with Python 2.7 and 3.x versions. PyMySQL is favored because it's simple, doesn't need extra software, and supports secure SSL connections. This makes it a great choice for Python applications needing to work with databases.

## Installing PyMySQL

To install PyMySQL, simply open your terminal or command prompt and enter the following command:

```bash
pip install pymysql
```
Once the installation process is complete, you'll be all set to harness the capabilities of Python-docx in your projects. So go ahead and execute the command, and let's get started with the exciting world of working with Word documents using Python!

## Connecting with MySQL

Use pymysql.connect() to establish a connection to your MySQL database. You'll need to provide details such as the hostname (or IP address), database username, password, and the database name you wish to connect to.

```python
import pymysql
connection = pymysql.connect(host='your_host',
                             user='your_username',
                             password='your_password',
                             database='your_database')
```

In case you do not want to specify the database name while creating the connection object, you can use the `select_db` method of the connection object to select the database.

```python
import pymysql
connection = pymysql.connect(host='your_host',
                             user='your_username',
                             password='your_password')
connection.select_db('your_database')
```

## Understanding the cursor object
In PyMySQL, the `cursor` object is a crucial component when working with databases. It represents a pointer or handle to the result set of a query that is executed on the database. The cursor object allows you to interact with the database, fetch rows, execute queries, and manage transactions.

## Creating a cursor object
To create a cursor, use the `cursor` method of the connection object:

```python
cursor = connection.cursor()
```

With the code above, we are now all set to execute queries and fetch results from MySQL.

## Executing Queries

To execute a query, we use the `execute` method of the cursor object.

```python
cursor.execute('Your Query')
```

Let's take an example. Assume you want to perform the below operations using PyMySQL.

```sql
USE testdb;
DROP TABLE IF EXISTS countries;
CREATE TABLE countries(
    id INT PRIMARY KEY AUTO_INCREMENT, 
    country_name VARCHAR(255), 
    capital VARCHAR(255), 
    capital_population INT
);

INSERT INTO countries(country_name, capital, capital_population) VALUES('Slovakia', 'Bratislava', 432000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('Hungary', 'Budapest', 1759000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('Czech Republic', 'Prague', 1280000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('Poland', 'Warsaw', 1748000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('United States', 'Washington, D.C.', 705749);
INSERT INTO countries(country_name, capital, capital_population) VALUES('Germany', 'Berlin', 3671000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('United Kingdom', 'London', 8982000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('France', 'Paris', 2161000);
INSERT INTO countries(country_name, capital, capital_population) VALUES('India', 'New Delhi', 29399141);

```

Here's how you can perform the above operations using PyMySQL:

```python
# Select test_db
connection.select_db('testdb')

# Create table countries
create_table_command = """
DROP TABLE IF EXISTS countries;
CREATE TABLE countries(
    id INT PRIMARY KEY AUTO_INCREMENT, 
    country_name VARCHAR(255), 
    capital VARCHAR(255), 
    capital_population INT
);
"""
cursor.execute(create_table_command)

# List of values to insert into the table
countries_data = [
    ('Slovakia', 'Bratislava', 432000),
    ('Hungary', 'Budapest', 1759000),
    ('Czech Republic', 'Prague', 1280000),
    ('Poland', 'Warsaw', 1748000),
    ('United States', 'Washington, D.C.', 705749),
    ('Germany', 'Berlin', 3671000),
    ('United Kingdom', 'London', 8982000),
    ('France', 'Paris', 2161000),
    ('India', 'New Delhi', 29399141)
]

# Insert into table
insert_command = "INSERT INTO countries (country_name, capital, capital_population) VALUES (%s, %s, %s)"
for country in countries_data:
    cursor.execute(insert_command, country)

# Commit the changes to the database
connection.commit()
```
As you can see it's fairly simple to perform operations on the database using PyMySQL. Notice the `connection.commit()` line, in PyMySQL, `connection.commit()` is used to commit the current transaction. All the changes made by the SQL statements in the transaction become visible to other database connections after a commit is executed. If you don't explicitly call `connection.commit()`, the changes you made during the transaction will not be saved to the database. This is particularly important for operations that modify data, like `INSERT`, `UPDATE`, or `DELETE` statements.

## Fetching results

Another use of the cursor object is to fetch results from the database. 

To fetch results from a table using PyMySQL, you can utilize different methods provided by the cursor object. Each method serves a specific purpose in retrieving data. Here's how you can use them:

- `fetchone()`: This method retrieves the next row of a query result set and returns a single sequence(tuple), or None when no more data is available.

- `fetchall()`: This method fetches all (remaining) rows of a query result, returning them as a tuple of tuples. This can be memory-intensive if the result set is large.

- `fetchmany(size)`: This method fetches the next set of rows of a query result, returning a tuple of tuples. size specifies the number of rows to fetch.

Here's an example Python script demonstrating these methods:

- `fetchone()`
    ```python
    cursor.execute("SELECT * FROM countries")

    # Fetch one row using fetchone()
    print("Fetch one row:")
    row = cursor.fetchone()
    while row is not None:
        print(row)
        row = cursor.fetchone()
    ```

    Output:

    ```bash
    Fetch one row:
    (1, 'Slovakia', 'Bratislava', 432000)
    (2, 'Hungary', 'Budapest', 1759000)
    (3, 'Czech Republic', 'Prague', 1280000)
    (4, 'Poland', 'Warsaw', 1748000)
    (5, 'United States', 'Washington, D.C.', 705749)
    (6, 'Germany', 'Berlin', 3671000)
    (7, 'United Kingdom', 'London', 8982000)
    (8, 'France', 'Paris', 2161000)
    (9, 'India', 'New Delhi', 29399141)
    ```
- `fetchall()`

    ```python
    # Re-execute the query to reset the cursor position
    cursor.execute("SELECT * FROM countries")

    # Fetch all rows using fetchall()
    print("Fetch all rows:")
    rows = cursor.fetchall()
    for row in rows:
        print(row)
    ```

    Output:
    ```bash
    Fetch all rows:
    (1, 'Slovakia', 'Bratislava', 432000)
    (2, 'Hungary', 'Budapest', 1759000)
    (3, 'Czech Republic', 'Prague', 1280000)
    (4, 'Poland', 'Warsaw', 1748000)
    (5, 'United States', 'Washington, D.C.', 705749)
    (6, 'Germany', 'Berlin', 3671000)
    (7, 'United Kingdom', 'London', 8982000)
    (8, 'France', 'Paris', 2161000)
    (9, 'India', 'New Delhi', 29399141)
    ```

- `fetchmany(size)`

    ```python
    # Re-execute the query to reset the cursor position
    cursor.execute("SELECT * FROM countries")

    # Fetch several rows using fetchmany()
    print("\nFetch many rows:")
    rows = cursor.fetchmany(3)
    for row in rows:
        print(row)
    ```

    Output:
    ```bash
    Fetch many rows:
    (1, 'Slovakia', 'Bratislava', 432000)
    (2, 'Hungary', 'Budapest', 1759000)
    (3, 'Czech Republic', 'Prague', 1280000)
    ```

## Closing the connection

Each open connection to a database uses resources both on the application side and the database server side. By closing the connection when it's no longer needed, you free up these resources, which can improve the performance of both the application and the database server. You can close a connection as follows:

```python
connection.close()
```

## Project Ideas

PyMySQL can be used for a variety of use cases and projects, making it a versatile tool for working with MySQL. Here are some examples of projects and use cases where PyMySQL can be applied:

- **Inventory Management System:** Develop a system for businesses to manage their stock, including features to track inventory levels, sales, orders, and suppliers.

- **School Management System:** Create a system for schools to manage student records, grades, attendance, and teacher assignments.

- **E-commerce Website Backend:** Develop the backend for an e-commerce website, handling product listings, user accounts, shopping carts, and order processing.

- **Booking and Reservation System:** An application for booking appointments or making reservations, such as for hotels or restaurants.

## FAQs

Here are some FAQ's about PyMySQL
<details>
<summary>What is PyMySQL</summary>
PyMySQL is a library in Python that enables you to interact with MySQL databases. It allows you to connect to a MySQL database, execute SQL queries, and manage data.
</details>

<details>
<summary>How is PyMySQL different from MySQLdb?</summary>
PyMySQL is written entirely in Python and is a pure-Python MySQL client, whereas MySQLdb is a C module that needs to be compiled against MySQL. PyMySQL is often used as a MySQLdb replacement and is compatible with Python 3.
</details>

<details>
<summary>How do you install PyMySQL?</summary>
You can install PyMySQL using pip: <code>pip install pymysql</code>. This is the standard method for installing Python packages.
</details>

<details>
<summary>Is PyMySQL compatible with MySQL and MariaDB?</summary>
Yes, PyMySQL works with both MySQL and MariaDB databases. It's designed to be a drop-in replacement for MySQLdb, which is compatible with these databases.
</details>

<details>
<summary>How do you handle transactions in PyMySQL?</summary>
Transactions in PyMySQL are managed through the connection object. After executing your queries, you use <code>connection.commit()</code> to commit the transaction or <code>connection.rollback()</code> to roll back the transaction.
</details>

<details>
<summary>What is the purpose of the cursor in PyMySQL?
</summary>
A cursor is a Python object that allows you to execute MySQL queries and retrieve results. It provides methods like <code>execute()</code>, <code>fetchone()</code>, <code>fetchall()</code>, and <code>fetchmany()</code> for these purposes.
</details>

<details>
<summary>How do you manage database connections in PyMySQL?
?</summary>
Database connections should be properly opened and closed to manage resources efficiently. Use pymysql.connect() to open a connection and connection.close() to close it. It’s a good practice to use Python's with statement or try-except-finally blocks to ensure connections are closed even when an error occurs.
</details>

<details>
<summary>Can you use PyMySQL for complex queries and stored procedures?</summary>
Yes, PyMySQL supports executing complex SQL queries, including joins, subqueries, and stored procedures. You can execute any SQL command that MySQL supports.</details>

## Related Articles

Here are some articles about **PyMySQL** that you may find helpful

<ul>
  <li> https://piptrends.com/package/pymysql </li>
  <li> https://pymysql.readthedocs.io/en/latest/ </li>
  <li> https://pypi.org/project/pymysql/ </li>
  <li> https://towardsdatascience.com/pymysql-connecting-python-and-sql-for-data-science-91e7582d21d7 </li>
  <li> https://medium.com/swlh/python-mysql-baby-steps-with-pymysql-89d62191f312 </li>
  <li> https://www.geeksforgeeks.org/connect-to-mysql-using-pymysql-in-python/ </li>
  <li> https://www.syncfusion.com/blogs/post/sql-a-complete-guide-for-beginners.aspx </li>

In this article, we have explored the PyMySQL library, which empowers users to interact with MySQL databases effortlessly. With the knowledge you've gained from this article, you're well-equipped to start integrating MySQL databases into your Python applications. From setting up connections and executing queries to fetching results and managing transactions, PyMySQL covers all the essentials you need for database operations. Plus, with the project ideas provided, you have a great starting point to explore and apply these skills in real-world scenarios.

Remember, the key to mastering PyMySQL, like any library, lies in practice and experimentation. Don't hesitate to try out new ideas and build your own unique applications using this versatile library. Also, always remember to close a connection when it is no longer needed and free up resources. Happy coding!

