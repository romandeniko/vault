---
created: 2025-09-29T18:05:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SELECT name, city, date_first, per_diem * (DATEDIFF(date_last, date_first) + 1) AS Сумма
FROM trip
WHERE (MONTH(date_first) = 2 OR MONTH(date_first) = 3) AND YEAR(date_first) = 2020
ORDER BY name ASC, Сумма DESC;
```































