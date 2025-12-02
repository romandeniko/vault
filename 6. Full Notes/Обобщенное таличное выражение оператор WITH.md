---
created: 2025-11-22
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
WITH название_cte [(столбец_1 [, столбец_2 ] …)] AS (подзапрос)
    [, название_cte [(столбец_1 [, столбец_2 ] …)] AS (подзапрос)] …
```

```sql
-- Пример использования конструкции WITH
WITH Aeroflot_trips AS
    (SELECT TRIP.* FROM Company
        INNER JOIN Trip ON Trip.company = Company.id WHERE name = 'Aeroflot')

SELECT plane, COUNT(plane) AS amount FROM Aeroflot_trips GROUP BY plane;
```































