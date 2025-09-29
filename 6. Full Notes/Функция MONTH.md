---
created: 2025-09-29T17:34:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Для того, чтобы выделить номер месяца из даты используется функция `MONTH(дата)`.

Например, `MONTH('2020-04-12') = 4`.

Если определяется месяц для  значений столбца `date_first`, то используется запись `MONTH(date_first)`

```sql
SELECT name, city, date_first, date_last
FROM trip
WHERE MONTH(date_first) = MONTH(date_last)
ORDER BY city ASC, name ASC;
```





























