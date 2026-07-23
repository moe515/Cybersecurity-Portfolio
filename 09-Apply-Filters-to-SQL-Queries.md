# Apply Filters to SQL Queries

---

## Project Description

As a security professional at a large organization, I investigated potential security issues involving login attempts and employee machines. I used SQL filters with the AND, OR, and NOT operators to retrieve specific records from the `log_in_attempts` and `employees` tables in the organization's database. This helped identify suspicious activity and determine which employee machines needed security updates.

---

## Retrieve After Hours Failed Login Attempts

I needed to identify all failed login attempts that occurred after business hours (after 18:00).

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;
```

**Explanation:** This query retrieves all records from the `log_in_attempts` table where the `login_time` is after 18:00 AND the `success` column equals 0 (indicating a failed attempt). The AND operator ensures both conditions must be true for a record to be returned.

---

## Retrieve Login Attempts on Specific Dates

A suspicious event occurred on 2022-05-09. I needed to review all login attempts on that day and the day before (2022-05-08).

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

**Explanation:** This query retrieves all records where the `login_date` is either 2022-05-09 OR 2022-05-08. The OR operator returns records that match either condition, allowing me to investigate both days at once.

---

## Retrieve Login Attempts Outside of Mexico

The suspicious activity was determined not to have originated in Mexico. I needed to find all login attempts from outside Mexico.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**Explanation:** This query uses NOT to exclude records where the `country` column matches the pattern `MEX%`. The LIKE keyword with the `%` wildcard covers both `MEX` and `MEXICO` values in the database. The NOT operator returns all records that do NOT match Mexico.

---

## Retrieve Employees in Marketing

The team needed to update machines for employees in the Marketing department located in the East building.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

**Explanation:** This query filters for employees whose `department` is exactly 'Marketing' AND whose `office` starts with 'East'. The LIKE keyword with the `%` wildcard matches all East building offices (East-170, East-320, etc.). The AND operator ensures both conditions must be met.

---

## Retrieve Employees in Finance or Sales

The team needed to update machines for employees in either the Sales or Finance departments.

```sql
SELECT *
FROM employees
WHERE department = 'Sales' OR department = 'Finance';
```

**Explanation:** This query retrieves all employees whose `department` is either 'Sales' OR 'Finance'. The OR operator returns records that match either condition, allowing the team to identify all affected employees in both departments at once.

---

## Retrieve All Employees Not in IT

The final update needed to be applied to all employees except those in the Information Technology department.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**Explanation:** This query uses the NOT operator to exclude all employees in the 'Information Technology' department. It returns every employee record where the `department` does not equal 'Information Technology', ensuring the IT department's already-updated machines are not included.

---

## Summary

In this project, I used SQL filters to investigate security issues and identify employees needing machine updates. I applied AND, OR, and NOT operators along with the LIKE keyword and % wildcard to filter data across the `log_in_attempts` and `employees` tables. These queries helped the security team identify suspicious after-hours login activity, investigate specific dates, trace login attempts by location, and target the correct employee machines for security updates.
