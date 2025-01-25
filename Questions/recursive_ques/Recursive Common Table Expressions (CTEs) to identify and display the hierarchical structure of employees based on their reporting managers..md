
In this SQL problem-solving session, we delve into the concept of determining employee hierarchy levels within an organization. Using real-world data, we demonstrate how to leverage Recursive Common Table Expressions (CTEs) to identify and display the hierarchical structure of employees based on their reporting managers.


```
📌 Table creation & insertion script:
CREATE TABLE emp_det ( emp_id INT, emp_name VARCHAR(50), emp_dep VARCHAR(50), emp_salary INT, emp_mgr_id INT );


INSERT INTO emp_det (emp_id, emp_name, emp_dep, emp_salary, emp_mgr_id) VALUES (10, 'Aarti', 'IT', 10000, NULL), (40, 'Vijay', 'IT', 8000, 10), (20, 'Devendra', 'IT', 5000, 40), (30, 'Jyoti', 'IT', 5000, 40), (60, 'Ajit', 'IT', 3000, 20);
```

Solution:

```sql

with cte as(
    select  emp_id,emp_name,emp_dep,emp_salary,emp_mgr_id, 0 as emp_level
    from emp_det
    where emp_mgr_id is null
	UNION all
    SELECT e.emp_id, e.emp_name, e.emp_dep,e.emp_salary,e.emp_mgr_id, emp_level + 1 as emp_level
    from emp_det e join cte c
    on e.emp_mgr_id = c.emp_id
)

SELECT * from cte;
```
