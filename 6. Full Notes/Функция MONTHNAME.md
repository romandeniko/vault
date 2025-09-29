---
created: 2025-09-29T17:43:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SELECT MONTHNAME(date_first) as Месяц, COUNT(date_first) AS Количество
FROM trip
GROUP BY MONTHNAME(date_first)
ORDER BY Количество DESC, Месяц ASC;
```
































