---
created: 2025-12-21
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
**Синтаксис:**
```sql
CASE
    WHEN условие_1 THEN возвращаемое_значение_1
    WHEN условие_2 THEN возвращаемое_значение_2
    WHEN условие_n THEN возвращаемое_значение_n
    [ELSE возвращаемое_значение_по_умолчанию]
END
```

**Пример:**
```sql
SELECT first_name, last_name,
CASE
  WHEN EXTRACT(YEAR FROM AGE(NOW(), birthday)) >= 18 THEN 'Совершеннолетний'
  ELSE 'Несовершеннолетний'
END AS status
FROM Student
```

```sql
SELECT name,
CASE
  WHEN SUBSTRING(name, 1, POSITION(' ' IN name) - 1) IN ('10', '11') THEN 'Старшая школа'
  WHEN SUBSTRING(name, 1, POSITION(' ' IN name) - 1) IN ('5', '6', '7', '8', '9') THEN 'Средняя школа'
  ELSE 'Начальная школа'
END AS stage
FROM Class
```

```sql
SELECT name,
CASE SUBSTRING(name, 1, POSITION(' ' IN name) - 1)
  WHEN '11' THEN 'Старшая школа'
  WHEN '10' THEN 'Старшая школа'
  WHEN '9' THEN 'Средняя школа'
  WHEN '8' THEN 'Средняя школа'
  WHEN '7' THEN 'Средняя школа'
  WHEN '6' THEN 'Средняя школа'
  WHEN '5' THEN 'Средняя школа'
  ELSE 'Начальная школа'
END AS stage
FROM Class
```




























