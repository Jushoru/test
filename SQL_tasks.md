**Задание 1**

Напишите запрос, который выведет сотрудника с максимальной заработной платой.
```
SELECT * FROM employee
WHERE salary = (SELECT MAX(salary) FROM employee)
```

**Задание 2**

Напишите запрос, который выведет одно число: максимальную длину цепочки руководителей по таблице сотрудников (вычислить глубину дерева).
```
WITH RECURSIVE rec AS (
SELECT id, chief_id, 1 AS tree_length FROM employee 
WHERE chief_id IS NULL
UNION
SELECT employee.id, employee.chief_id, rec.tree_length + 1 FROM employee
JOIN rec ON employee.chief_id = rec.id
) SELECT MAX(tree_length) FROM rec

```

**Задание 3**

Напишите запрос, который выведет отдел, с максимальной суммарной зарплатой сотрудников.
```
SELECT sum, name FROM (SELECT SUM(employee.salary), department.* FROM employee
JOIN department ON employee.department_id = department.id
GROUP BY employee.department_id, department.id)
ORDER BY sum DESC LIMIT 1

```

**Задание 4**

Напишите запрос, который выведет сотрудника, чье имя начинается на «Р» и заканчивается на «н».
```
SELECT * FROM employee
WHERE name LIKE 'Р%н'
```

