# Filter with `AND`, `OR` and `NOT` in SQL

> **Note:** This practical lab activity was completed using Qwiklabs as part of the **Google Cybersecurity Professional Certificate**.

> **Note:** Query outputs and screenshots display truncated sample rows, as full result sets contained extensive logs.

---
## Scenario
In this activity, I investigate potential security issues and identify specific computer assets for updates across departments. I need to extract targeted authentication records from the `log_in_attempts` table and staff details from the `employees` table in the organisation database.

To do this, I will write advanced SQL queries using logical operators (`AND`, `OR`, `NOT`) and pattern matching (`LIKE`) to filter records across multiple criteria.

---
## Task 1: Retrieve After-Hours Failed Login Attempts
My team needed to investigate unsuccessful login attempts occurring outside normal business hours (after 18:00).

I ran the following query using the `AND` operator to combine two strict conditions—ensuring that both the timestamp was after 18:00 and the login was recorded as a failure (`success = 0`):

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_time > '18:00' AND success = 0;
```
<img width="790" height="460" alt="Screenshot 2026-09-01 191746" src="https://github.com/user-attachments/assets/3ef5d2ef-5ec0-4a8c-a124-bc7e1dacb733" />

* **Why I used these commands/operators:**
  * `WHERE login_time > '18:00'`: Filters for timestamps strictly following the close of business.
  * `AND`: Enforces that both criteria must be met simultaneously for a row to be returned.
  * `success = 0`: MariaDB stores Booleans numerically (`1` for TRUE, `0` for FALSE); setting this to `0` isolates only the failed attempts.

---
## Task 2: Retrieve Login Attempts on Specific Dates
Next, I investigated a security event linked to `2022-05-09` by auditing all login attempts that occurred on that day as well as the preceding day (`2022-05-08`).

I executed the following query using the `OR` operator:

```sql

SELECT *
    -> FROM log_in_attempts
    -> WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```
<img width="792" height="290" alt="Screenshot 2026-09-01 192020" src="https://github.com/user-attachments/assets/6460f7f9-3f90-4c49-8947-f52973c2b12f" />

* **Why I used these commands/operators:**
  * `OR`: Broadens the search so records matching either the target date or the day before are captured in a single output.

---

## Task 3: Retrieve Login Attempts Outside of Mexico
My team required an audit of logins that did not originate from Mexico. The `country` column contains multiple naming formats such as `MEX` and `MEXICO`.

I filtered out these records by combining the `NOT` operator with `LIKE` and the `%` wildcard:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE NOT country LIKE 'MEX%';
```
<img width="795" height="272" alt="Screenshot 2026-09-01 192208" src="https://github.com/user-attachments/assets/1f8735fa-b654-4847-92bc-f0d7881c6da7" />

* **Why I used these commands/operators:**
  * `LIKE 'MEX%'`: Matches any country entry beginning with the string "MEX" (catching both `MEX` and `MEXICO`).
  * `NOT`: Inverts the match condition to exclude all Mexican traffic and return only entries from other countries (e.g. `CAN`, `USA`).

---

## Task 4: Retrieve Marketing Employees in the East Building
To support scheduled machine updates, I needed to locate all staff members within the Marketing department who work in any office within the East building.

I executed the following query on the `employees` table:

```sql
SELECT *
    -> FROM employees
    -> WHERE department = 'Marketing' AND office LIKE 'East%';
```

<img width="603" height="255" alt="Screenshot 2026-09-01 193601" src="https://github.com/user-attachments/assets/89e64561-cf6d-44f3-a33f-0d1d05ceb77d" />

* **Why I used these commands/operators:**
  * `WHERE department = 'Marketing'`: Restricts the returned records to the Marketing department.
  * `AND`: Requires both the department and the building location to match.
  * `LIKE 'East%'`: Uses the wildcard `%` to capture every room number within the East facility (such as `East-170`, `East-195`).

---

## Task 5: Retrieve Employees in Finance or Sales
My team needed an asset inventory for staff in either the Finance or Sales departments to perform an update roll-out.

I used the `OR` operator to query both teams together:

```sql
SELECT *
    -> FROM employees
    -> WHERE department = 'Finance' OR department = 'Sales';
```
<img width="636" height="257" alt="Screenshot 2026-09-01 193816" src="https://github.com/user-attachments/assets/6bb48ef8-62ac-457b-8ac9-9e32ac9437a0" />

* **Why I used these commands/operators:**
  * `OR`: Allows the query to return employee rows belonging to either the Finance department or the Sales department in one list.

---

## Task 6: Retrieve All Employees Not in IT
A final software update had already been deployed to the Information Technology department, so I needed a list of all remaining employees across the organisation who still required the update.

I ran the following query using the `NOT` operator

```sql
SELECT *
    -> FROM employees
    -> WHERE NOT department = 'Information Technology';
```

<img width="662" height="238" alt="Screenshot 2026-09-01 194001" src="https://github.com/user-attachments/assets/b29badda-afef-460c-af3c-45e104778dcf" />

* **Why I used these commands/operators:**
  * `NOT`: Negates the equality match, filtering out all IT staff while returning records for every other department (such as Marketing, Human Resources, Finance, and Sales).

---

## Summary
In this activity, I applied complex SQL filtering logic to investigate logs and manage system updates:
* I used `AND` to combine multiple conditions, such as isolating failed after-hours authentication attempts (`login_time > '18:00' AND success = 0`) and narrowing employee locations by department and office building (`department = 'Marketing' AND office LIKE 'East%'`).
* I used `OR` to return records matching either of two criteria, including multi-date log queries and multi-department asset reviews.
* I applied `NOT` to invert conditions, successfully excluding specific geographic regions with pattern matching (`NOT country LIKE 'MEX%'`) and filtering out previously updated departments (`NOT department = 'Information Technology'`).







