---
title: NIVEL 3 — Introducción a análisis (Agregaciones)
sidebar_position: 3
---

---
### 16. Contar usuarios por role.
```sql
SELECT role, COUNT(*) AS total_users
FROM users
GROUP BY role;
```
---
### 17. Contar usuarios por document_type.
```sql
SELECT document_type, COUNT(*) AS total_users
FROM users
GROUP BY document_type;
```
---
### 18. Contar cuántos usuarios están desempleados.
```sql
SELECT COUNT(*) AS usuarios_desempleados
FROM users
WHERE company IS NULL;
```
---
### 19. Calcular el promedio general de ingresos.
Version 1:
```sql
SELECT AVG(monthly_income)
FROM users;
```

Version 2: AVG ignora los nullos, pero mejor especificar
```sql
SELECT AVG(monthly_income)
FROM users
WHERE monthly_income IS NOT NULL;
```
---
### 20. Calcular el promedio de ingresos por role.
```sql
SELECT role, AVG(monthly_income) AS average_income
FROM users
GROUP BY role;
```
