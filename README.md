---

# FitPro Gym SQL Project

![Fitpro_logo](https://github.com/user-attachments/assets/69348c5d-eec6-4978-9f96-ecc7f26e0aab)


Welcome to my first SQL project, where I analyze real-time gym data from **FitPro Gym**! This project uses a dataset of **10,000 visit records** to explore and analyze gym membership and visit data, answering key business questions that can help a fitness center understand it's customer base better and optimize its services.

## Table of Contents
- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Business Problems](#business-problems)
- [SQL Queries & Analysis](#sql-queries--analysis)
- [Getting Started](#getting-started)
- [Questions & Feedback](#questions--feedback)
- [Contact Me](#contact-me)

---

## Introduction

This project aims to demonstrate essential SQL skills by analyzing a dataset from FitPro Gym. Using SQL, I explored membership details, member demographics, and visit patterns to derive actionable insights. This project showcases fundamental SQL techniques, including creating tables, writing queries, and analyzing data.

## Project Structure

1. **SQL Scripts**: Code to create the database schema and queries for analysis. 
2. **Dataset**: Real-time data on gym visits, membership, and member demographics.
3. **Analysis**: SQL queries solving practical business problems, each one crafted to address specific questions.

---

## Database Schema

Here’s an overview of the database structure:

### 1. **Members Table**
- **member_id**: Unique identifier for each member
- **name**: Name of the member

### 2. **Memberships Table**
- **member_id**: Unique identifier linked to the `members` table
- **age**: Age of the member
- **gender**: Gender of the member ('M' or 'F')
- **membership_type**: Type of membership (e.g., Monthly, Quarterly)
- **join_date**: Date when the member joined
- **status**: Membership status (e.g., Active, Cancelled)

### 3. **Visits Table**
- **visit_id**: Unique identifier for each visit
- **member_id**: Linked to the `members` table
- **visit_date**: Date of the visit
- **check_in_time**: Check-in time of the visit
- **check_out_time**: Check-out time of the visit

## Business Problems

The following queries were created to solve specific business questions. Each query is designed to provide insights based on gym membership and visit data.

1. Retrieve the **name** and **membership_type** of female members.
```sql
SELECT 
	ms.membership_type,
	ms.gender,
	m.name
FROM memberships ms
JOIN members m ON m.member_id = ms.member_id
WHERE gender = 'F';
``` 
2. Find members who have a **Monthly membership** and joined after **2023-11-01**.
```sql
SELECT *
FROM memberships
WHERE membership_type = 'Monthly'
	AND join_date >= '2023-11-01';
```
3. List the **name** and **status** of active members over **25**.
 ```sql
  SELECT 
	  m.name,
	  ms.status,
	  ms.age
  FROM memberships ms
  JOIN members m ON m.member_id = ms.member_id
  WHERE ms.status = 'Active'
	AND ms.age >= 25; 
 ```
5. Get details of **visits** on a specific date (**2024-01-01**).

```sql
 SELECT *
FROM VISITS
WHERE visit_date ='2024-01-01' 
```
6. List members with a **Quarterly membership** aged between **20 and 30**.
```sql
   SELECT * 
   FROM memberships
   WHERE membership_type = 'Monthly'
	  AND
	  age BETWEEN 20 AND 30;
```

Additional aggregations and grouping:

7. Count total visits made by each member.
```sql
  SELECT 
	member_id,
	visit_date,
	count(*) as total_visits
  FROM visits
  GROUP BY member_id, visit_date;
```
8. Count members by membership type (e.g., Monthly, Weekly, Quarterly).
```sql
  SELECT
	membership_type,
	count( membership_type)
  FROM memberships
  GROUP BY membership_type;
   ```
9. Calculate the average age of members, grouped by membership type.
  ```sql
  SELECT 
	membership_type,
	AVG(age) as average_age
  FROM memberships
  GROUP BY membership_type;
  ```

10. Total visits for each visit date.
    ```sql
    SELECT
	   visit_date,
	   count(visit_date)
    FROM visits
    GROUP BY visit_date;  
    ```
12. Count members by status (e.g., Active or Cancelled).
    ```sql
    SELECT 
	    status,
	    count (member_id)
    FROM memberships
    WHERE status  = 'Active'
    OR status = 'Cancelled'
    GROUP BY status;
    ```

Advanced queries:

11. Top 3 members with the highest visits.
```sql
SELECT
	member_id,
	count(visit_date)
FROM visits
GROUP BY 1
ORDER BY 2 DESC
LIMIT 3
```

12. Active Monthly members grouped by membership type, sorted by recent join dates.
```sql
SELECT
	status,
	join_date,
	membership_type,
	count(*) as Active_members
FROM memberships
WHERE status = 'Active'
	AND membership_type = 'Monthly'
GROUP BY 1, 2, 3
ORDER BY join_date DESC;
```

13. Members with more than 2 visits, sorted by total visits, displaying the top 5.
```sql
SELECT
	member_id,
	COUNT(distinct visit_date) as Total_visits
FROM visits
WHERE  member_id > 2
GROUP BY 1
ORDER BY COUNT(distinct visit_date) DESC
LIMIT 5
```

14. Members who joined in 2023, grouped by membership type (where each group has >1 member).
```sql
SELECT 
	membership_type, 
	COUNT(member_id) AS member_count 
FROM memberships 
WHERE date_part('year', join_date) = 2023 
GROUP BY membership_type 
HAVING COUNT(member_id) > 1;
```

15. Average age of active members, grouped by membership type, limited to the top 3 results.
```sql
SELECT
	membership_type,
	ROUND(AVG(age):: NUMERIC, 2) as avg_age
FROM memberships
WHERE status = 'Active'
group by 1
LIMIT 3
```
---

## SQL Queries & Analysis

The `analysis.sql` file contains all SQL queries developed for this project. Each query corresponds to a business problem and demonstrates skills in SQL syntax, data filtering, aggregation, grouping, and ordering.

## Getting Started

### Prerequisites
- PostgreSQL (or any SQL-compatible database)
- Basic understanding of SQL

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Jkusi6/SQL_FitPropjt.git
   ```
2. **Set Up the Database**:
   - Run the `schema.sql` script to set up tables and insert sample data.

3. **Run Queries**:
   - Execute each query in `analysis.sql` to explore and analyze the data.

---

## Questions & Feedback

If you have any questions or feedback, feel free to create an issue or reach out!


---

## Contact Me

📄 **[Resume]([Joré's Resume.docx](https://github.com/user-attachments/files/18272705/Jore.s.Resume.docx)
)**  
📧 **[Email](mailto:jorekusi@gmail.com)**  
📞 **Phone**: +1-313-707-1870  

--
