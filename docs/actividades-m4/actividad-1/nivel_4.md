---
title: NIVEL 4 — Pensamiento analítico
sidebar_position: 4
---

---
### 21. Mostrar profesiones con más de 10 personas.
Version 1:
```sql
SELECT COUNT(id) AS number_persons, profession
FROM users
WHERE profession IS NOT NULL
GROUP BY profession
HAVING COUNT(id) > 10;
```
Version 2:
```sql
SELECT profession, COUNT(*) AS number_persons
FROM users
WHERE profession IS NOT NULL
GROUP BY profession
HAVING COUNT(*) > 10;
```

---
### 22. Mostrar la ciudad con más usuarios.
Version 1:
```sql
SELECT COUNT(id) AS numer_users, city
FROM users
GROUP BY city
LIMIT 1;
```
Version 2:
```sql
SELECT city, COUNT(*) AS number_users
FROM users
GROUP BY city
ORDER BY number_users DESC
LIMIT 1;
```

---
### 23. Comparar cantidad de menores vs mayores de edad.

Version 1 (consultas separadas):
```sql
SELECT COUNT(id) AS majors
FROM users
WHERE birth_date < '2008-02-12';

SELECT COUNT(id) AS menors
FROM users
WHERE birth_date > '2008-02-12';
```
(usando SUM + CASE):
```sql
SELECT
    SUM(CASE WHEN birth_date < '2008-02-12' THEN 1 ELSE 0 END) AS adult,
    SUM(CASE WHEN birth_date > '2008-02-12' THEN 1 ELSE 0 END) AS minor
FROM users;
```
Version 2 (agrupado por categoría):
```sql
SELECT 
    CASE 
        WHEN birth_date < '2008-02-12' THEN 'adult'
        ELSE 'minor'
    END AS age_group,
    COUNT(*) AS quantity
FROM users
GROUP BY age_group;
```

---
### 24. Promedio de ingresos por ciudad ordenado de mayor a menor.
Version por estado:
```sql
SELECT state, AVG(monthly_income) AS promedio
FROM users
GROUP BY state
ORDER BY promedio DESC
LIMIT 5;
```

Version por ciudad:
```sql
SELECT city, AVG(monthly_income) AS promedio
FROM users
GROUP BY city
ORDER BY promedio DESC
LIMIT 5;
```
---

### 25. Mostrar las 5 personas con mayor ingreso.
Version 1 (sin agrupar, solo ordenar):
```sql
    SELECT first_name, monthly_income
    FROM users
    ORDER BY monthly_income DESC
    LIMIT 5;
```

Version 2 (agrupando por id):
```sql
SELECT id, first_name, monthly_income
FROM users
ORDER BY monthly_income DESC
LIMIT 5;
```
