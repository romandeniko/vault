---
created: 2025-10-02T19:32:00
status:
links:
  - "[[Базы данных]]"
  - "[[Запросы SQL]]"
  - "[[SQL]]"
---
```sql
SELECT name
FROM Passenger
WHERE LENGTH(name) = (SELECT MAX(LENGTH(name)) FROM Passenger);
```































