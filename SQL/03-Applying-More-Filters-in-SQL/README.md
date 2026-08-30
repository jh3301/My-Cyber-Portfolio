# Applying More Filters in SQL

> **Note:** This practical lab activity was completed using Qwiklabs as part of the **Google Cybersecurity Professional Certificate**.

> **Note:** Query outputs and screenshots display truncated sample rows, as full result sets contained extensive logs.

---
## Scenario
In this activity, I am investigating a recent security incident affecting the organisation. My objective is to gather specific authentication log data across targeted dates, times, and event IDs to identify potentially malicious or anomalous login activity.

To accomplish this investigation, I will query the `log_in_attempts` table in the MariaDB shell using comparison operators (`>`, `>=`, `<`) and range operators (`BETWEEN ... AND`).

---
## Task 1: Retrieve Login Attempts After a Certain Date
To investigate suspicious events following an initial security alert, I first needed to examine all authentication attempts made strictly after `2022-05-09`.

I executed the following query using the greater-than (`>`) comparison operator:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_date > '2022-05-09';
```
<img width="793" height="309" alt="Screenshot 2026-08-30 162343" src="https://github.com/user-attachments/assets/f5c35251-26ff-4002-852d-33b922d27341" />

Based on the initial results, I needed to expand my investigation scope to include events occurring on the day of `2022-05-09` itself. I modified the query using the greater-than-or-equal-to (`>=`) operator:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_date >= '2022-05-09';
```
<img width="791" height="291" alt="Screenshot 2026-08-30 162626" src="https://github.com/user-attachments/assets/ef5039b8-098b-46d3-ac32-e2d85000a0a1" />

This query successfully captured all relevant authentication activity beginning directly from 9 May 2022 onwards.

---

## Task 2: Retrieve Logins in a Specific Date Range
To narrow my investigation window and exclude unneeded logs generated after `2022-05-11`, I isolated activity occurring specifically between 9 May and 11 May 2022.

I ran the following query using the `BETWEEN` and `AND` operators:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';
```
<img width="793" height="237" alt="Screenshot 2026-08-30 162826" src="https://github.com/user-attachments/assets/6ce2e522-f8f1-418b-9610-b5e31eca54fd" />

Using `BETWEEN ... AND` ensured both boundary dates were included while filtering out any unrelated entries outside the incident timeframe.

---
## Task 3: Investigate Logins at Certain Times
Next, I investigated potential out-of-hours access. The organisation's standard business hours begin at `07:00:00`, so I queried for any authentication events occurring prior to typical working hours.

### Auditing Pre-Work-Hour Logins
I executed a query to find all login attempts recorded before `07:00:00` using the less-than (`<`) operator:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_time < '07:00';
```
<img width="790" height="277" alt="Screenshot 2026-08-30 184354" src="https://github.com/user-attachments/assets/6cba5956-2bd0-42ec-88f5-4a480e62ce34" />

### Narrowing the Pre-Shift Timeframe
Because the previous query returned an extensive volume of entries spanning midnight onwards, I refined the search window to focus specifically on logins occurring between `06:00:00` and `07:00:00`:

```sql
SELECT *
    -> FROM log_in_attempts
    -> WHERE login_time BETWEEN '06:00' AND '07:00';
```
<img width="797" height="395" alt="Screenshot 2026-08-30 184529" src="https://github.com/user-attachments/assets/062b4c26-777d-4b1a-b74c-be38659c4821" />

This isolated 15 distinct login attempts occurring just before the start of business, highlighting both successful access and failed attempts (such as users `eraab`, `mcouliba`, and `gesparza`).

---
## Task 4: Investigate Logins by Event ID
In this task, I focused my investigation on specific log entries using numerical event identifiers.

### Filtering for Event IDs Greater Than or Equal to 100
I first filtered for records starting from event ID 100 onwards, selecting only the necessary columns (`event_id`, `username`, and `login_date`):

```sql
MariaDB [organization]> SELECT event_id, username, login_date
    -> FROM log_in_attempts
    -> WHERE event_id >= 100;
```
<img width="567" height="241" alt="Screenshot 2026-08-30 185132" src="https://github.com/user-attachments/assets/d44b5398-3058-4ef0-a6a6-e71fc0edd2b6" />

### Restricting Event IDs to a Bounded Range
To focus on a specific segment of the log sequence, I restricted the query to return only event IDs between 100 and 150:

```sql
MariaDB [organization]> SELECT event_id, username, login_date
    -> FROM log_in_attempts
    -> WHERE event_id BETWEEN 100 AND 150;
```
<img width="556" height="293" alt="Screenshot 2026-08-30 185249" src="https://github.com/user-attachments/assets/733b7a64-f0eb-435d-86c1-03941b787b78" />

This returned a concise list of target events without pulling extraneous log records.

---

## Summary
In this activity, I applied advanced SQL filtering techniques to investigate security log records:
* I used comparison operators (`>`, `>=`, `<`) to isolate login activity across temporal thresholds.
* I applied the `BETWEEN ... AND` operator across both date and time fields to examine specific anomaly windows.
* I filtered numerical data types to isolate specific batches of authentication records by `event_id`.




































