# Performing a SQL Query

## Lab Activity & Investigation Report — Database Querying Fundamentals

In this lab activity, I used the fundamental SQL commands `SELECT` and `FROM` to retrieve specific information from an organisation's relational database. I also utilised the `ORDER BY` clause to sequence the returned query records based on specified columns in ascending order.

## Scenario 

In this scenario, I needed to determine which employee devices require operating system updates and patches. Additionally, I investigated user login activity to identify whether any unusual activity or security anomalies occurred across the network.

The relevant records are stored across two tables within the **`organisation`** database:

<img width="706" height="226" alt="Screenshot 2026-08-26 151810" src="https://github.com/user-attachments/assets/d9ab6a22-73a4-474d-93d9-41ddfd480b40" />

## Task 1: Retrieve Employee Device Data

In this task, I needed to obtain information on employee devices because my team needs to coordinate operating system updates. All necessary hardware data is located in the `machines` table.

### 1.1 Selecting All Device Information

First, I retrieved all device information by running a query to select all columns from the `machines` table:

```sql
SELECT *
FROM machines;
```
<img width="742" height="272" alt="Screenshot 2026-08-26 152545" src="https://github.com/user-attachments/assets/bc439458-f12a-495b-a513-840ae252e096" />

* Using `SELECT` indicates which columns to display. Here, the asterisk wildcard (`*`) denotes that all columns should be returned (`SELECT ALL`).
* The `FROM` keyword indicates the table where the data is stored (the `machines` table).
* The semicolon (`;`) indicates the termination of the query statement.

### 1.2 Focusing on Specific Email Clients

Next, I narrowed the query to focus specifically on the email clients running across various employee devices. I executed the following query, separating the desired columns with a comma:

```sql
SELECT device_id, email_client
FROM machines;
```
<img width="487" height="345" alt="Screenshot 2026-08-26 130819" src="https://github.com/user-attachments/assets/f3492a49-02e3-4ef5-9b38-f72e7b8ad578" />

### 1.3 Reviewing Operating Systems and Patch Dates

To determine which systems required immediate patching, I ran a query to retrieve the operating system versions alongside their most recent patch dates:

```sql
SELECT device_id, operating_system, OS_patch_date
FROM machines;
```
<img width="665" height="308" alt="Screenshot 2026-08-26 131158" src="https://github.com/user-attachments/assets/b280f091-2c00-4d88-8dc0-3abf456e0713" />

## Task 2: Investigate Login Activity

In this task, I analysed data within the `log_in_attempts` table to determine whether any unusual login activity or security concerns had arisen.

### 2.1 Checking Geographic Locations

First, I investigated the locations from which login attempts originated to verify that they fell within expected regions (the United States, Canada, or Mexico), scanning manually for anomalies:

```sql
SELECT event_id, country
FROM log_in_attempts;
```
<img width="442" height="262" alt="Screenshot 2026-08-26 131424" src="https://github.com/user-attachments/assets/13ef6594-8ead-47ad-8dfe-0c6beb898818" />

### 2.2 Checking Login Timestamps

Next, I evaluated whether user login attempts were occurring outside of standard organisational working hours by running:

```sql
SELECT username, login_date, login_time
FROM log_in_attempts;
```
<img width="596" height="257" alt="Screenshot 2026-08-26 131732" src="https://github.com/user-attachments/assets/e69c69b4-fdaf-4aba-8976-dc6a54167fc2" />

### 2.3 Reviewing Full Login Attempt Details

To obtain a complete overview of all login records—including IP addresses and authentication outcomes—I selected all columns from the `log_in_attempts` table:

```sql
SELECT *
FROM log_in_attempts;
```
<img width="820" height="277" alt="Screenshot 2026-08-26 132019" src="https://github.com/user-attachments/assets/749949b1-068a-472d-8502-dbfca51073c7" />

## Task 3: Order Login Attempts Data

In this task, I utilised the `ORDER BY` clause to sequence and structure the returned dataset chronologically by login date and time.

### 3.1 Sorting by Date

First, I sorted the authentication records by date using the following query:

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date;
```
<img width="817" height="395" alt="Screenshot 2026-08-26 132346" src="https://github.com/user-attachments/assets/18f0f4a6-a45a-4df7-baed-1203d6604bd9" />

While this organised the events by calendar day, multiple logins occurring on the same date remained unsorted by time.

### 3.2 Multi-Column Ordering (Date and Time)

To establish a seamless chronological order across multiple dates and within each individual day, I applied multi-column sorting:

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date, login_time;
```
<img width="801" height="341" alt="Screenshot 2026-08-26 132618" src="https://github.com/user-attachments/assets/f35ac84a-17a3-4c87-8b89-58f2c3cfb4da" />

## Conclusion & Summary

Through this lab activity, I have gained practical hands-on experience in executing fundamental SQL queries to:
* **Select specific columns** from a table using explicit column names (e.g. `SELECT device_id, email_client`).
* **Select all columns** simultaneously using the asterisk (`*`) wildcard.
* **Sort query results** chronologically and systematically using single and multi-column `ORDER BY` clauses.

### Future Plan — Integrating the `WHERE` Clause:
This activity marks my starting point in database analysis. Sifting through unfiltered datasets of 200+ rows manually is time-consuming and inefficient for incident investigation. Moving forward, I will be incorporating the `WHERE` clause into queries to filter records by specific conditions (such as failed logins `WHERE success = 0` or overdue patches), eliminating manual searches and streamlining incident response.

















