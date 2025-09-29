---
created: 2025-09-27T13:56:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
```sql
SELECT author, sum(amount), count(amount)
FROM book
GROUP BY author;
```

Для `COUNT()` можно использовать любой столбец из группы, если группа не содержит пустых значений.

```sql
SELECT author, SUM(amount)
FROM book
GROUP BY author;
```

```sql
/* чтобы проверить запрос, добавьте в таблицу строку */
INSERT INTO book (title, author, price, amount) VALUES ('Черный человек','Есенин С.А.', Null, Null);

SELECT author, COUNT(author), COUNT(amount), COUNT(*)
FROM book
GROUP BY author;
```

_Результат:_

```sql
+------------------+---------------+---------------+----------+
| author           | COUNT(author) | COUNT(amount) | COUNT(*) |
+------------------+---------------+---------------+----------+
| Булгаков М.А.    | 2             | 2             | 2        |
| Достоевский Ф.М. | 3             | 3             | 3        |
| Есенин С.А.      | 2             | 1             | 2        |
+------------------+---------------+---------------+----------+
```

Из таблицы с результатами запроса видно, что функцию `**COUNT()**` можно применять к любому столбцу, в том числе можно использовать и `*`, если таблица не содержит пустых значений. Если же в столбцах есть значения `Null`, (для группы по автору Есенин в нашем примере), то

- `COUNT(*)` —  подсчитывает  все записи, относящиеся к группе, в том числе и со значением `**NULL**`;
- `COUNT(имя_столбца)` — возвращает количество записей конкретного столбца (только `NOT NULL`), относящихся к группе.

**ВАЖНО.**
1. Если столбец указан в `SELECT`  **БЕЗ** применения групповой функции, то он обязательно должен быть указан и в`GROUP BY.`Иначе получим ошибку.

```sql
SELECT author as Автор, COUNT(author) AS Различных_книг, SUM(amount) AS Количество_экземпляров
FROM book
GROUP BY author;
```

```sql
DELETE FROM supply
WHERE author IN (
    SELECT author
    FROM book
    GROUP BY author
    HAVING SUM(amount)> 10
);
```

```sql
SELECT city, COUNT(city) AS Количество
FROM trip
GROUP BY city
ORDER BY city ASC;
```

```sql
SELECT name, SUM(per_diem * (DATEDIFF(date_last, date_first) + 1)) AS Сумма
FROM trip
GROUP BY name
HAVING COUNT(name) > 3
ORDER BY Сумма DESC;
```























