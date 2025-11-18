---
created: 2025-11-04
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SET @row_num := 0;

SELECT *, (@row_num := @row_num + 1) AS str_num
FROM  applicant_order;
```

```sql
SET @num_pr := 0;
SET @row_num := 1;

SELECT *, 
     if(program_id = @num_pr, @row_num := @row_num + 1, @row_num := 1) AS str_num,
     @num_pr := program_id AS add_var 
from applicant_order;
```

```sql
SET @num_pr := 1;
SET @row_num := 0;

UPDATE applicant_order
SET str_id = IF(program_id = @num_pr, @row_num := @row_num + 1, @row_num := 1 AND @num_pr := @num_pr + 1);

SELECT * FROM applicant_order;
```
































