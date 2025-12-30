---
created: 2025-12-21
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Функция COALESCE - это элегантное решение для работы с NULL значениями. Она возвращает первое не-NULL значение из списка аргументов.

Использовать **COALESCE**: Когда нужно заменить NULL значения на значения по умолчанию.

**Синтаксис:**
```sql
COALESCE(значение1, значение2, ..., значениеN);
```

**Пример:**
```sql
SELECT COALESCE(NULL, NULL, 'SQL Academy', 'Запасной вариант') AS sql_trainer;
```

```sql
SELECT first_name, COALESCE(middle_name, 'Empty') as middle_name, last_name
FROM Teacher;
```




























