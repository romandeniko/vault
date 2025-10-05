---
created: 2025-10-02T18:45:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SELECT town_to, TIMEDIFF(time_in, time_out) AS flight_time
FROM Trip
WHERE town_from = 'Paris';
```































