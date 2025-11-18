---
created: 2025-11-09
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Извлекает часть даты (год, месяц, день и т.д.) для указанной даты

```sql
SELECT EXTRACT(YEAR FROM DATE '2022-06-16') AS year;
```

```sql
SELECT member_name, EXTRACT (YEAR FROM DATE(birthday)) AS year_of_birth FROM FamilyMembers;
```

```sql
EXTRACT(EPOCH FROM(time_in-time_out)
```

























