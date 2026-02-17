---
title: Nivel 1 - Fundamentos (Exploración básica)
sidebar_position: 1
---
---

### 1. Listar todos los usuarios
```sql
SELECT * FROM users
```
---
### 2. Mostrar solo first_name, last_name, email.
```sql
SELECT first_name, last_name, email
FROM users;
``` 
---
### 3. Filtrar usuarios cuyo role sea 'admin'.
```sql
SELECT * FROM users WHERE role = 'admin'
```
---
### 4. Filtrar usuarios con document_type = 'CC'.
```sql
SELECT *
FROM users
WHERE document_type = 'CC'
```
---
### 5. Mostrar usuarios mayores de 18 años
```sql
SELECT *
FROM users
WHERE birth_date < '2008-02-12'
```
Opción mas precisa empleando TIMESTAMPDIFF, YEAR, CURDATE()
```sql
SELECT *
FROM users
WHERE TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) >= 18;
```
---
### 6. Mostrar usuarios cuyo ingreso sea mayor a 5,000,000.
```sql
SELECT * 
FROM users 
WHERE monthly_income > 5000000
```
---
### 7. Mostrar usuarios cuyo nombre empiece por "A".
```sql
SELECT * 
FROM users 
WHERE first_name 
like 'A%'
```
---
### 8. Mostrar usuarios que no tengan company.
```sql
SELECT * 
FROM users 
WHERE company IS NULL 
```

