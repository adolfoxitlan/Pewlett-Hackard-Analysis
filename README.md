# Pewlett-Hackard-Analysis.
Postgres Analsysis.

## Deliverable 1.

Using the ERD you created in this module as a reference and your knowledge of SQL queries, create a Retirement Titles table that holds all the titles of current employees who were born between January 1, 1952 and December 31, 1955. Because some employees may have multiple titles in the database—for example, due to promotions—you’ll need to use the DISTINCT ON statement to create a table that contains the most recent title of each employee. Then, use the COUNT() function to create a final table that has the number of retirement-age employees by most recent job title.

 - [x] 1 A query is written and executed to create a Retirement Titles table for employees who are born between January 1, 1952 and December 31, 1955 (10 pt)
 - [x] 2 The Retirement Titles table is exported as retirement_titles.csv
 - [x] 3  A query is written and executed to create a Unique Titles table that contains the employee number, first and last name, and most recent title.
 - [x] 4 The Unique Titles table is exported as unique_titles.csv
 - [x] 5 A query is written and executed to create a Retiring Titles table that contains the number of titles filled by employees who are retiring.
 - [x] 6 The Retiring Titles table is exported as retiring_titles.csv

### 1 - A query is written and executed to create a Retirement Title ...

QUERY.

    SELECT e.emp_no,
           e.first_name,
           e.last_name,
           t.title,
           t.from_date,
           t.to_date
    INTO retirement_titles
    FROM employees as e
    INNER JOIN titles as t
    ON (e.emp_no = t.emp_no)
    WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
    order by e.emp_no;

### 2 - The Retirement Titles table is exported as retirement_titles.csv ...
[retirement_titles.csv](https://github.com/adolfoxitlan/Pewlett-Hackard-Analysis/blob/97c8536d2ad3dda7f32f9fe571dc5b8be930c002/Data/retirement_titles.csv)

### 3 - A query is written and executed to create a Unique Titles ...

    SELECT DISTINCT ON (emp_no) emp_no,
    first_name,
    last_name,
    title
    INTO unique_titles
    FROM retirement_titles
    ORDER BY emp_no, title DESC;

### 4 - The Retirement Titles table is exported as unique_titles.csv ...
[unique_titles.csv](Data/unique_titles.csv)

### 5 - A query is written and executed to create a Retiring Titles ...

    SELECT COUNT(ut.emp_no),
    ut.title
    INTO retiring_titles
    FROM unique_titles as ut
    GROUP BY title 
    ORDER BY COUNT(title) DESC;
    
### 6 - The Retirement Titles table is exported as unique_titles.csv ...
[retiring_titles.csv](Data/retiring_titles.csv)



