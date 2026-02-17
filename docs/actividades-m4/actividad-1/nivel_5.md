---
title: NIVEL 5 — Nivel Ingeniero
sidebar_position: 5
---


### 26. Clasificar usuarios como "Menor", "Adulto", "Adulto mayor".
Version 1:
```sql
SELECT first_name, birth_date,
CASE 
    WHEN birth_date < '2008-02-12' AND birth_date > '1964-02-12' THEN 'adult'
    WHEN birth_date > '2008-02-12' THEN 'young'
    WHEN birth_date < '1964-02-12' THEN 'old'
END AS age
FROM users;
```

Version 2:
```sql
SELECT first_name, birth_date,
CASE 
    WHEN birth_date > DATE_SUB(CURDATE(), INTERVAL 18 YEAR) THEN 'Menor'
    WHEN birth_date BETWEEN 
         DATE_SUB(CURDATE(), INTERVAL 60 YEAR)
         AND DATE_SUB(CURDATE(), INTERVAL 18 YEAR) THEN 'Adulto'
    ELSE 'Adulto mayor'
END AS age_group
FROM users;
```

---
### 27. Mostrar cuántos usuarios hay en cada clasificación anterior.

Version 1:
```sql
SELECT
CASE 
    WHEN birth_date < '2008-02-12' AND birth_date > '1964-02-12' THEN 'adult'
    WHEN birth_date > '2008-02-12' THEN 'young'
    ELSE 'old'
END AS age,
COUNT(*) AS number_age
FROM users
GROUP BY age;
```

Version 2:
```sql
SELECT
CASE 
    WHEN birth_date > DATE_SUB(CURDATE(), INTERVAL 18 YEAR) THEN 'Menor'
    WHEN birth_date BETWEEN 
         DATE_SUB(CURDATE(), INTERVAL 60 YEAR)
         AND DATE_SUB(CURDATE(), INTERVAL 18 YEAR) THEN 'Adulto'
    ELSE 'Adulto mayor'
END AS age_group,
COUNT(*) AS total_users
FROM users
GROUP BY age_group;
```

---
### 28. Ranking de ingresos por ciudad.
Version 1:
```sql
SELECT city, monthly_income AS ingresos
FROM users
WHERE monthly_income IS NOT NULL
ORDER BY ingresos DESC
LIMIT 10;
```
Version 2:
```sql
SELECT city, AVG(monthly_income) AS average_income
FROM users
WHERE monthly_income IS NOT NULL
GROUP BY city
ORDER BY average_income DESC;
```

---
### 29. Profesión con mayor ingreso promedio.
Version 1:
```sql
SELECT profession, AVG(monthly_income) AS income_avg
FROM users
GROUP BY profession
ORDER BY income_avg DESC
LIMIT 1;
```
Version 2:
```sql
SELECT profession, AVG(monthly_income) AS income_avg
FROM users
GROUP BY profession
ORDER BY income_avg DESC
LIMIT 5;
```

---
### 30. Mostrar usuarios cuyo ingreso esté por encima del promedio general.
Forma manual:
```sql
SELECT first_name, monthly_income
FROM users
WHERE monthly_income >= 7861517.176895;
```
Forma correcta (subconsulta):
```sql
SELECT first_name, monthly_income
FROM users
WHERE monthly_income > (
    SELECT AVG(monthly_income)
    FROM users
);
```

Segunda opción (clasificando):
```sql
SELECT first_name, monthly_income,
CASE
    WHEN monthly_income > (
        SELECT AVG(monthly_income)
        FROM users
    ) THEN 'mas'
    ELSE 'menos'
END AS comparative_promedio
FROM users
WHERE monthly_income IS NOT NULL
ORDER BY monthly_income DESC;
```