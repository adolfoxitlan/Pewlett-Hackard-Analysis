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


## Deliverable 3: A written report on the employee database Analysis.
 
- Overview of the analysis.

Now that Bobby has proven his SQL chops, his manager has given both of you two more assignments: determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. Then, you’ll write a report that summarizes your analysis and helps prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age. 

- Results.

Provide a bulleted list with four major points from the two analysis deliverables.

Deliverable 1:
- There is a high percetange of employee that could retire at any time.
- Important to mention that engineer postions are in the top 5 titles of the retiring_title.csv, those titles are hard to fill.

      - 32,452 Staff
      - 29,415 Senior Engineer
      - 14,221 Engineer
      - 8,047 Senior Staff
      - 4,502 Technique Leader
      - 1,761 Assistant Engineer

- Summary.

Provide high-level responses to the following questions, then provide two additional queries or tables that may provide more insight into the upcoming "silver tsunami.":

1) How many roles will need to be filled as the "silver tsunami" begins to make an impact?.
- 90,398 roles.

2) Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
- No, 1,940 are junior employee, eigible for mentorship.

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


