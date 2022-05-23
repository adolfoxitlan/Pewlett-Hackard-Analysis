# Pewlett-Hackard-Analysis.
Postgres Analsysis.

## Deliverable 1.

Using the ERD you created in this module as a reference and your knowledge of SQL queries, create a Retirement Titles table that holds all the titles of current employees who were born between January 1, 1952 and December 31, 1955. Because some employees may have multiple titles in the database—for example, due to promotions—you’ll need to use the DISTINCT ON statement to create a table that contains the most recent title of each employee. Then, use the COUNT() function to create a final table that has the number of retirement-age employees by most recent job title.

 - [x] 1 A query is written and executed to create a Retirement Titles table for employees who are born between January 1, 1952 and December 31, 1955.
 - [x] 2 The Retirement Titles table is exported as retirement_titles.csv.
 - [x] 3  A query is written and executed to create a Unique Titles table that contains the employee number, first and last name, and most recent title.
 - [x] 4 The Unique Titles table is exported as unique_titles.csv
 - [x] 5 A query is written and executed to create a Retiring Titles table that contains the number of titles filled by employees who are retiring.
 - [x] 6 The Retiring Titles table is exported as retiring_titles.csv.

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

### 2 - The Retirement Titles table is exported as retirement_titles.csv.
[retirement_titles.csv](Data/retirement_titles.csv)

### 3 - A query is written and executed to create a Unique Titles ...

QUERY.

    SELECT DISTINCT ON (emp_no) emp_no,
    first_name,
    last_name,
    title
    INTO unique_titles
    FROM retirement_titles
    ORDER BY emp_no, title DESC;

### 4 - The Retirement Titles table is exported as unique_titles.csv.
[unique_titles.csv](Data/unique_titles.csv)

### 5 - A query is written and executed to create a Retiring Titles ...

QUERY.

    SELECT COUNT(ut.emp_no),
    ut.title
    INTO retiring_titles
    FROM unique_titles as ut
    GROUP BY title 
    ORDER BY COUNT(title) DESC;
    
### 6 - The Retirement Titles table is exported as unique_titles.csv.
[retiring_titles.csv](Data/retiring_titles.csv)



## Deliverable 2.

Using the ERD you created in this module as a reference and your knowledge of SQL queries, create a mentorship-eligibility table that holds the current employees who were born between January 1, 1965 and December 31, 1965.

 - [x] 1 A query is written and executed to create a Mentorship Eligibility table for current employees who were born between January 1, 1965 and December 31, 1965.
 - [x] 2 The Mentorship Eligibility table is exported and saved as mentorship_eligibilty.csv.


### 1 - A query is written and executed to create a Mentorship Eligibility ...

QUERY.

    SELECT DISTINCT ON(e.emp_no) e.emp_no, 
        e.first_name, 
        e.last_name, 
        e.birth_date,
        de.from_date,
        de.to_date,
        t.title
    INTO mentorship_eligibilty
    FROM employees as e
    Left outer Join dept_emp as de
    ON (e.emp_no = de.emp_no)
    Left outer Join titles as t
    ON (e.emp_no = t.emp_no)
    WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
    ORDER BY e.emp_no;
    
### 2 - The Retirement Titles table is exported as mentorship_eligibilty.csv.
[mentorship_eligibilty.csv](Data/mentorship_eligibilty.csv)
