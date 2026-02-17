---
title: Nivel 2 - Combinación de condiciones
sidebar_position: 2
---
---

### 9. Usuarios mayores de 25 años que sean 'employee'.
version 1:
```sql
SELECT *
FROM users
WHERE birth_date < '2001-02-12'
    AND role = 'employee';
```
Version mas precisa
```sql
SELECT *
FROM users
WHERE birth_date <= DATE_SUB(CURDATE(), INTERVAL 25 YEAR)
    AND role = 'employee';
```
---
### 10. Usuarios con 'CC' que estén activos.
```sql
SELECT *
FROM users
WHERE document_type = 'CC'
    AND is_active = 1;
```
---
### 11. Usuarios mayores de edad sin empleo.
```sql
SELECT *
FROM users
WHERE birth_date < '2008-02-12'
    AND company IS NULL;
```
version 2:
```sql
SELECT *
FROM users
WHERE birth_date <= DATE_SUB(CURDATE(), INTERVAL 18 YEAR)
    AND company IS NULL;
```
---
### 12. Usuarios con empleo y con ingresos mayores a 3,000,000.
```sql
SELECT *
FROM users
WHERE company IS NOT NULL
    AND monthly_income > 3000000;
```
---
### 13. Usuarios casados con al menos 1 hijo.
```sql
SELECT *
FROM users
WHERE marital_status = 'Casado'
    AND children_count >= 1;
```
---
### 14. Usuarios entre 30 y 40 años.
```sql
SELECT *
FROM users
WHERE birth_date > '1986-02-12'
    AND birth_date < '1996-02-12';
```
Version 2:
```sql
SELECT *
FROM users
WHERE birth_date BETWEEN 
    DATE_SUB(CURDATE(), INTERVAL 40 YEAR)
    AND DATE_SUB(CURDATE(), INTERVAL 30 YEAR);

```
---
### 15. Usuarios 'admin' verificados mayores de 25 años.
```sql
SELECT *
FROM users
WHERE role = 'admin'
    AND is_verified = 1
    AND birth_date < '2001-02-12';
```
Version 2:
```sql
SELECT *
FROM users
WHERE role = 'admin'
    AND is_verified = 1
    AND birth_date <= DATE_SUB(CURDATE(), INTERVAL 25 YEAR);

```
