---
created: 2025-11-08
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
INSERT INTO step_keyword (step_id, keyword_id)
SELECT step.step_id, keyword.keyword_id
FROM step
CROSS JOIN keyword
WHERE  
INSTR(CONCAT(" ", step.step_name, " "), CONCAT(" ", keyword.keyword_name, " ")) > 0 OR
INSTR(CONCAT(" ", step.step_name, " "), CONCAT(" ", keyword.keyword_name, ",")) > 0 OR
INSTR(CONCAT(" ", step.step_name, " "), CONCAT(" ", keyword.keyword_name, "(")) > 0
ORDER BY keyword.keyword_id;
SELECT*FROM step_keyword;
```
































