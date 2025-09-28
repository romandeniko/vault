---
created: 2025-09-26T20:35:00
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
![[Оператор LIKE.png]]

```sql
SELECT title 
FROM book
WHERE title LIKE 'Б%';
/* эквивалентное условие 
title LIKE 'б%'
*/
```

```sql
SELECT title FROM book 
WHERE title LIKE "_____"               /* вывести названия книг из 5 букв
```

```sql
SELECT title FROM book 
WHERE title LIKE "______%";
/* эквивалентные условия 
title LIKE "%______"
title LIKE "%______%"
*/
```

```sql
SELECT title FROM book 
WHERE   title LIKE "_% и _%" /*отбирает слово И внутри названия */
    OR title LIKE "и _%" /*отбирает слово И в начале названия */
    OR title LIKE "_% и" /*отбирает слово И в конце названия */
    OR title LIKE "и" /* отбирает название, состоящее из одного слова И */
```

```sql
SELECT title FROM book 
WHERE title NOT LIKE "% %";  
```

```sql
SELECT title, author
FROM book
WHERE title LIKE "%_ _%" AND author LIKE "%С.%"
ORDER BY title;
```

```sql
SELECT name, city, per_diem, date_first, date_last
FROM trip
WHERE name LIKE '%а %'
ORDER BY date_last DESC; 
```

	



















