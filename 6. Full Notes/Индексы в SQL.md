---
created: 2026-07-23T21:00:00
status:
links:
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Позволяют быстро находить информацию в таблице.
### Синтаксис
```sql
CREATE INDEX idx_email
    ON Users (email);
```

### Отображение индексов
```sql
SELECT indexname, indexdef
FROM pg_indexes
WHERE tablename = 'users';
```

### Удаление индекса
```sql
DROP INDEX idx_email;
```

### Уникальные индексы
```sql
CREATE UNIQUE INDEX idx_email
    ON Users (email);
```

При попытке добавить пользователя с уже существующим адресом, будет ошибка:
```sql
ERROR: duplicate key value violates unique constraint "idx_email"
DETAIL: Key (email)=(duplicate@gmail.com) already exists.
```

### Многостолбцовые индексы
```sql
CREATE INDEX idx_full_name
    ON Student (last_name, first_name);
```


























