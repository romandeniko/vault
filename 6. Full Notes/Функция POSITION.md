---
created: 2025-11-09
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Осуществляет поиск подстроки в строке, возвращая позицию её первого символа. При этом отсчёт начинается с единицы, а не нуля, как в большинстве языков программирования.

```sql
SELECT POSITION('academy' IN 'sql-academy') AS idx;
```

```sql
SELECT member_name,
	LENGTH(member_name) AS full_length,
	POSITION(' ' IN member_name) AS firstname_with_space_length,
	LENGTH(member_name) - POSITION(' ' IN member_name) AS lastname_length
FROM FamilyMembers;
```





























