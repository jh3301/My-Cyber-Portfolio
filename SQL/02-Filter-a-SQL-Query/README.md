# Filtering a SQL Query

> **Note:** This practical lab activity was completed using Qwiklabs as part of the **Google Cybersecurity Professional Certificate**.

> **Note:** Query outputs and screenshots display truncated sample rows, as full result sets contained up to 200 records.

## Scenario
In this activity, I need to retrieve specific information about employees, their assigned machines, and their departments from the organisation database. My security team needs this data to identify machines requiring operating system updates, notify staff in specific departments regarding confidential data handling policies, and locate an employee linked to a hardware issue in the South building.

To accomplish this efficiently, I will query the database using `SELECT` and `FROM` statements combined with `WHERE` filtering clauses and pattern matching via the `LIKE` operator.

---

## Inspecting Database Schema
Before executing filtered queries, I first inspected the table structures in the `organisation` database using the `DESCRIBE` command:

```sql
DESCRIBE machines;
DESCRIBE employees;
```

<img width="598" height="397" alt="Screenshot 2026-08-29 174629" src="https://github.com/user-attachments/assets/8b044def-17c8-4c49-80fe-335e4b5253a5" />

## Task 1: List All Organisation Machines

My first task is to generate a comprehensive list of all company machines alongside their operating systems to get visibility into what OS versions are deployed across the fleet.

I ran the following query to extract only the `device_id` and `operating_system` columns from the `machines` table

```sql
SELECT device_id, operating_system
    -> FROM machines;
```
<img width="533" height="325" alt="Screenshot 2026-08-29 175155" src="https://github.com/user-attachments/assets/96f99114-3c23-4ca0-8eae-8bb9e713fe3f" />

This query successfully returned all machine records with their respective operating system labels (e.g. `OS 1`, `OS 2`, `OS 3`).

---
## Task 2: Retrieve a List of Machines Running OS 2

My team determined that all devices running the `OS 2` operating system require a critical update[cite: 4]. I needed to isolate only these devices from the database.

To filter for these specific assets, I appended a `WHERE` clause checking for the exact string value `'OS 2'`:

```sql
SELECT device_id, operating_system
    -> FROM machines
    -> WHERE operating_system = 'OS 2';
```

<img width="531" height="273" alt="Screenshot 2026-08-29 175611" src="https://github.com/user-attachments/assets/a4e830b0-fbee-4f89-ac6b-9578dc99c81f" />


By filtering with `WHERE operating_system = 'OS 2'`, the query excluded all unrelated OS records and provided my team with an actionable inventory of machines needing the update (such as `a192b174c940`, `a320b137c219`, `a821b452c176`, and `b157c491d493`).

---

## Task 3: List Employees in Specific Departments

In this task, I needed to retrieve office locations for employees working in the Finance and Sales departments so that security notices regarding confidential financial handling procedures could be posted to their respective offices.

### Filtering for Finance Department Employees
I first filtered the `employees` table to return all staff members belonging to the `Finance` department:

```sql
SELECT *
    -> FROM employees
    -> WHERE department = 'Finance';
```

<img width="632" height="343" alt="Screenshot 2026-08-29 175834" src="https://github.com/user-attachments/assets/3a6ad00b-1c23-482b-b25d-d5bce55e9cc9" />

This returned all records for Finance personnel, identifying office locations such as `South-153`, `North-406`, `South-170`, and `South-109`.

### Filtering for Sales Department Employees
Next, I modified the query to target the `Sales` department:

```sql
SELECT *
    -> FROM employees
    -> WHERE department = 'Sales';
```

<img width="625" height="277" alt="Screenshot 2026-08-29 180005" src="https://github.com/user-attachments/assets/53e99a44-935d-42e1-a00c-ef018cd02be0" />

This query returned all staff within the Sales organisation along with their assigned office numbers across South, North, East, and Central facilities.

---

## Task 4: Identify Employee Machines and South Building Assets
My team identified technical issues impacting hardware in the South building[cite: 4]. I was tasked with isolating the specific employee in office `South-109`, followed by retrieving all personnel located in the South facility[cite: 4].

### Locating the User in Office South-109
To identify who uses the computer in `South-109`, I executed a query filtering the `office` column:

```sql
SELECT *
    -> FROM employees
    -> WHERE office = 'South-109';
```

<img width="600" height="157" alt="Screenshot 2026-08-29 180201" src="https://github.com/user-attachments/assets/5f34a571-1545-47ae-a73f-ed8ffcc7530e" />

The result showed employee `1010` (username `jlansky`, Finance department, device `k2421212m542`), allowing our team to send an alert directly to the affected user.

### Pattern Matching All Offices in the South Building
Because multiple machines across the entire South building experienced faults, I updated the query to return all staff located in any South office[cite: 4]. Since office names follow the convention `Building-Number` (e.g. `South-109`, `South-153`), I utilised the `LIKE` operator with the `%` wildcard:

```sql
SELECT *
    -> FROM employees
    -> WHERE office LIKE 'South%';
```
<img width="708" height="315" alt="Screenshot 2026-08-29 180320" src="https://github.com/user-attachments/assets/318e762a-ec5d-4cdd-b229-6b3524e7a22b" />

The `LIKE 'South%'` condition successfully matched every office beginning with "South", giving my team a complete list of all employees and assigned device IDs across the entire building.

## Summary
In this activity, I applied SQL query filtering techniques to extract targeted security and asset data:
* I used `DESCRIBE` to review database schemas and understand column definitions across the `machines` and `employees` tables.
* I used `SELECT` and `FROM` to retrieve specific columns for hardware inventory audits.
* I applied the `WHERE` clause with exact string matching to isolate machines running `OS 2` and identify personnel in the `Finance` and `Sales` departments.
* I used the `LIKE` operator with the `%` wildcard to perform pattern matching across office identifiers in the South facility.







