Sure! Here’s a clear, professional README for your project that explains what it does, how to set it up, and how to run it:

---

# SQL Server Data Analysis with PySpark

This project demonstrates how to connect to a Microsoft SQL Server database using PySpark, run complex queries by joining multiple tables, and perform data analysis tasks such as ranking customer orders and checking room availability.

---

## Features

* **Connect to SQL Server** via JDBC with PySpark, using the official Microsoft JDBC driver.
* Execute SQL queries and load data from multiple related tables (`orders`, `customers`, `order_details`, `services`, `service_types`, etc.).
* Perform advanced data transformations and aggregations with PySpark DataFrame API, including window functions.
* Calculate ranked customer orders with detailed service information.
* Check guesthouse room availability based on booking dates and outlet filters.
* Modular functions to easily customize queries by customer ID, outlet ID, or date ranges.

---

## Prerequisites

* Python 3.7+
* Apache Spark 3.x installed
* Microsoft SQL Server JDBC Driver (e.g. `mssql-jdbc-12.10.0.jre8.jar`)
* Access credentials for a Microsoft SQL Server instance with required tables

---

## Setup

1. **Download the Microsoft SQL Server JDBC Driver**
   Download the driver from the [official Microsoft site](https://learn.microsoft.com/en-us/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server) and update the `jar_path` variable in the script with the path to the `.jar` file.

2. **Configure database connection**
   Update the `sql_server_db_config` dictionary in the script with your SQL Server hostname/IP, database name, username, and password.

```python
sql_server_db_config = {
    'server': '<your_server>',
    'user': '<your_username>',
    'password': '<your_password>',
    'database': '<your_database>'
}
```

3. **Install dependencies**
   Make sure you have PySpark installed:

```bash
pip install pyspark
```

---

## Usage

* The script connects to the SQL Server database using the provided JDBC URL and credentials.
* It verifies the connection by running a test query.
* Contains two main functions:

### `get_ranked_customer_orders(customerID=None, outletID=None)`

Retrieves orders joined with customer, service, and service type data, then ranks service prices per order by date.

* Filters results by optional `customerID` and/or `outletID`.
* Returns a PySpark DataFrame with detailed order and service info plus rank.

Example usage:

```python
ranked_orders_df = get_ranked_customer_orders(customerID=285, outletID=None)
ranked_orders_df.show()
```

---

### `get_guesthouse_room_availability(startdate, enddate, outletID)`

Checks room availability by joining services with orders and bookings, filtering for rooms booked within the given date range and outlet.

* Returns a DataFrame indicating which rooms are booked or available.

Example usage:

```python
available_rooms_df = get_guesthouse_room_availability('2025-05-01', '2025-05-10', 3)
available_rooms_df.show()
```

---

## Notes

* The script uses Spark’s JDBC connector and requires the JDBC driver `.jar` in the classpath.
* You can modify or extend the SQL queries inside each function for more complex business logic.
* The date filters and outlet/customer filters allow you to tailor the analysis for specific needs.

---

## Troubleshooting

* **Driver Not Found:** Make sure the `jar_path` correctly points to the JDBC driver `.jar` file.
* **Connection Errors:** Verify SQL Server is accessible and the credentials are correct.
* **Spark Configuration:** Ensure Spark and PySpark are properly installed and configured.

---




