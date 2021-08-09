# Pewlett-Hackard-Analysis_Challenge
Module 7 Challenge

## Overview of the Pewlett-Hackard-Analysis

### Background

> Bobby's require to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program.

### Purpose

Prepare Bobby's manager for the "silver tsunami" as many current employees reach retirement age.

## Results

   1. Number of Retiring Employees by Title: Code
 
```
    SELECT count(ut.title), ut.title
    INTO retiring_titles
    FROM unique_titles as ut
    GROUP BY ut.title
    ORDER BY count(ut.title) DESC;
```
 
   2. Seven roles in which the retiring will be affecting
   
   ![Retiring_titles](https://user-images.githubusercontent.com/86028032/128666907-ff4ec892-2b13-4ba0-8018-38224ccb5df5.PNG)

   
   3. Employees Eligible for the Mentorship Program: Code

```
   SELECT DISTINCT ON (e.emp_no) e.emp_no,
                      e.first_name,
                      e.last_name,
                      e.birth_date,
                      de.from_date,
                      de.to_date,
                      ti.title
   INTO mentorship_eligibilty
   FROM employees as e
   INNER JOIN dept_emp as de
   ON (e.emp_no = de.emp_no)
   INNER JOIN titles as ti
   ON (e.emp_no = ti.emp_no)
   WHERE de.to_date = ('9999-01-01')
   AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
   ORDER BY e.emp_no ASC, ti.to_date DESC;
```

   4. There are 1549 retirement-ready employees in the departments to mentor.

```
Select count(me.emp_no)
FROM mentorship_eligibilty as me
```

## Summary

+ How many roles will need to be filled as the "silver tsunami" begins to make an impact?

  + There will be seven roles to be filled as the "silver tsunami" begins to make an impact; 
      + Code for gotting the number of roles to be filled:
      
      ![Code_quantity_roles_to_be_filled](https://user-images.githubusercontent.com/86028032/128665238-51f88560-f647-4fd1-b1a2-5bc1e4f1301c.PNG)
      
       + Roles that required to be filled :
       
       ![Quantity_roles_to_be_filled](https://user-images.githubusercontent.com/86028032/128665401-52e214bc-a5e0-4f80-a325-22e4e1477dea.PNG)


  
  + Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

       + Yes, most of the retirement-ready employees are senior employees which are able to mentoring the next generation.
        
       ![Retiring_titles](https://user-images.githubusercontent.com/86028032/128665626-dae133d5-a5f8-46b0-b651-7947e2e2f471.PNG)

        

