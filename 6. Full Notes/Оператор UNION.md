---
created: 2025-10-11T16:13:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
**Оператор UNION**

Оператор `**UNION**` используется для объединения двух и более SQL запросов, его синтаксис:

```sql
SELECT столбец_1_1, столбец_1_2, ...
FROM 
  ...
UNION
SELECT столбец_2_1, столбец_2_2, ...
FROM 
  ...
```

или

```sql
SELECT столбец_1_1, столбец_1_2, ...
FROM 
  ...
UNION ALL
SELECT столбец_2_1, столбец_2_2, ...
FROM 
  ...
```

Важно отметить, что каждый из `**SELECT**` должен иметь в своем запросе одинаковое количество столбцов и  совместимые типы возвращаемых данных. Каждый запрос может включать разделы `**WHERE**`, `**GROUP BY**` и пр.

В результате выполнения этой конструкции будет выведена таблица, имена столбцов которой соответствуют именам столбцов в первом запросе. А в таблице результата сначала отображаются записи-результаты первого запроса, а затем второго. Если указано ключевое слово `**ALL**`, то в результат включаются все записи запросов, в противном случае - различные.

**Пример**

Вывести всех клиентов, которые делали заказы или в этом, или в предыдущем году.

На этом примере рассмотрим разницу между `**UNION**` и `**UNION ALL**`.

С `**UNION**` клиенты будут выведены без повторений:

```sql
SELECT name_client
FROM 
    buy_archive
    INNER JOIN client USING(client_id)
UNION
SELECT name_client
FROM 
    buy 
    INNER JOIN client USING(client_id)
+-----------------+
| name_client     |
+-----------------+
| Баранов Павел   |
| Абрамова Катя   |
| Яковлева Галина |
| Семенонов Иван  |
+-----------------+
Affected rows: 4
```

C `**UNION ALL**` будут выведены клиенты с повторением (для тех, кто заказывал книги в обоих годах, а также несколько раз в одном году)

```sql
SELECT name_client
FROM 
    buy_archive
    INNER JOIN client USING(client_id)
UNION ALL
SELECT name_client
FROM 
    buy 
    INNER JOIN client USING(client_id)
+-----------------+
| name_client     |
+-----------------+
| Баранов Павел   |
| Баранов Павел   |
| Абрамова Катя   |
| Абрамова Катя   |
| Абрамова Катя   |
| Яковлева Галина |
| Яковлева Галина |
| Баранов Павел   |
| Абрамова Катя   |
| Абрамова Катя   |
| Баранов Павел   |
| Баранов Павел   |
| Абрамова Катя   |
| Семенонов Иван  |
+-----------------+
Affected rows: 14
```

**Пример**

Вывести информацию об оплаченных заказах за предыдущий и текущий год, информацию отсортировать по  `**client_id**`.

_Запрос:_

```sql
SELECT buy_id, client_id, book_id, date_payment, amount, price
FROM 
    buy_archive
UNION ALL
SELECT buy.buy_id, client_id, book_id, date_step_end, buy_book.amount, price
FROM 
    book 
    INNER JOIN buy_book USING(book_id)
    INNER JOIN buy USING(buy_id) 
    INNER JOIN buy_step USING(buy_id)
    INNER JOIN step USING(step_id)                  
WHERE  date_step_end IS NOT Null and name_step = "Оплата"  
```  
_Результат:_

```sql
+--------+-----------+---------+--------------+--------+--------+
| buy_id | client_id | book_id | date_payment | amount | price  |
+--------+-----------+---------+--------------+--------+--------+
| 2      | 1         | 1       | 2019-02-21   | 2      | 670.60 |
| 2      | 1         | 3       | 2019-02-21   | 1      | 450.90 |
| 1      | 2         | 2       | 2019-02-10   | 2      | 520.30 |
| 1      | 2         | 4       | 2019-02-10   | 3      | 780.90 |
| 1      | 2         | 3       | 2019-02-10   | 1      | 450.90 |
| 3      | 4         | 4       | 2019-03-05   | 4      | 780.90 |
| 3      | 4         | 5       | 2019-03-05   | 2      | 480.90 |
| 4      | 1         | 6       | 2019-03-12   | 1      | 650.00 |
| 5      | 2         | 1       | 2019-03-18   | 2      | 670.60 |
| 5      | 2         | 4       | 2019-03-18   | 1      | 780.90 |
| 1      | 1         | 3       | 2020-02-20   | 1      | 460.00 |
| 1      | 1         | 7       | 2020-02-20   | 2      | 570.20 |
| 1      | 1         | 1       | 2020-02-20   | 1      | 670.99 |
| 2      | 3         | 8       | 2020-02-28   | 2      | 518.99 |
| 3      | 2         | 1       | 2020-03-05   | 1      | 670.99 |
| 3      | 2         | 2       | 2020-03-05   | 1      | 540.50 |
| 3      | 2         | 3       | 2020-03-05   | 2      | 460.00 |
+--------+-----------+---------+--------------+--------+--------+
```

В результат включены сначала записи архивной таблицы, а затем информация об оплаченных заказах  текущего года. Для того, чтобы изменить порядок следования записей в объединенном запросе, можно использовать **сортировку** по всем объединенным записям. В этом случае ключевые слова `**ORDER BY**` указываются после последнего запроса: 

```sql
SELECT buy_id, client_id, book_id, date_payment, amount, price
FROM 
    buy_archive
UNION ALL
SELECT buy.buy_id, client_id, book_id, date_step_end, buy_book.amount, price
FROM 
    book 
    INNER JOIN buy_book USING(book_id)
    INNER JOIN buy USING(buy_id) 
    INNER JOIN buy_step USING(buy_id)
    INNER JOIN step USING(step_id)                  
WHERE  date_step_end IS NOT Null and name_step = "Оплата"
ORDER BY client_id
```

_Результат:_

```sql
+--------+-----------+---------+--------------+--------+--------+
| buy_id | client_id | book_id | date_payment | amount | price  |
+--------+-----------+---------+--------------+--------+--------+
| 2      | 1         | 3       | 2019-02-21   | 1      | 450.90 |
| 2      | 1         | 1       | 2019-02-21   | 2      | 670.60 |
| 1      | 1         | 3       | 2020-02-20   | 1      | 460.00 |
| 1      | 1         | 7       | 2020-02-20   | 2      | 570.20 |
| 4      | 1         | 6       | 2019-03-12   | 1      | 650.00 |
| 1      | 1         | 1       | 2020-02-20   | 1      | 670.99 |
| 3      | 2         | 1       | 2020-03-05   | 1      | 670.99 |
| 3      | 2         | 2       | 2020-03-05   | 1      | 540.50 |
| 3      | 2         | 3       | 2020-03-05   | 2      | 460.00 |
| 5      | 2         | 4       | 2019-03-18   | 1      | 780.90 |
| 5      | 2         | 1       | 2019-03-18   | 2      | 670.60 |
| 1      | 2         | 3       | 2019-02-10   | 1      | 450.90 |
| 1      | 2         | 4       | 2019-02-10   | 3      | 780.90 |
| 1      | 2         | 2       | 2019-02-10   | 2      | 520.30 |
| 2      | 3         | 8       | 2020-02-28   | 2      | 518.99 |
| 3      | 4         | 5       | 2019-03-05   | 2      | 480.90 |
| 3      | 4         | 4       | 2019-03-05   | 4      | 780.90 |
+--------+-----------+---------+--------------+--------+--------+
```

```sql
SELECT YEAR(date_payment) AS Год, MONTHNAME(date_payment) AS Месяц, SUM(price * amount) AS Сумма
FROM 
    buy_archive
GROUP BY Год, Месяц
UNION ALL
SELECT YEAR(date_step_end) AS Год, MONTHNAME(date_step_end) AS Месяц, SUM(price * buy_book.amount) AS Сумма
FROM book
     INNER JOIN buy_book ON book.book_id = buy_book.book_id
     INNER JOIN buy_step ON buy_book.buy_id = buy_step.buy_id
WHERE step_id = 1 AND date_step_end IS NOT NULL
GROUP BY Год, Месяц
ORDER BY Месяц ASC;
```

```sql
SELECT result.title, SUM(Количество) AS Количество, SUM(Сумма) AS Сумма
FROM (
SELECT title, SUM(buy_archive.amount) AS Количество, SUM(buy_archive.amount * buy_archive.price) AS Сумма
FROM buy_archive
     INNER JOIN book ON buy_archive.book_id = book.book_id
GROUP BY title
UNION ALL
SELECT title, SUM(buy_book.amount) AS Количество, SUM(buy_book.amount * book.price) AS Сумма
FROM book
     INNER JOIN buy_book ON book.book_id = buy_book.book_id
     INNER JOIN buy_step ON buy_book.buy_id = buy_step.buy_id
WHERE step_id = 1 AND date_step_end IS NOT NULL
GROUP BY title
    )result
GROUP BY title
ORDER BY Количество DESC, Сумма DESC;
```



























