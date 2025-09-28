---
created: 2025-09-27T14:09:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SELECT author, MIN(price) AS min_price
FROM book
GROUP BY author;
```

```sql
SELECT author, MIN(price) AS Минимальная_цена, MAX(price) AS Максимальная_цена, AVG(price) AS Средняя_цена
FROM book
GROUP BY author;
```






























