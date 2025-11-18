---
created: 2025-10-24
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Позволяет соединить две строки

```sql
CONCAT("ab","cd") -> "abcd"
```

```sql
SELECT name_subject, CONCAT(LEFT(name_question, 30), "...") AS Вопрос, COUNT(answer_id) AS Всего_ответов, ROUND(SUM((SELECT IF(answer_id IN (SELECT answer_id FROM answer WHERE is_correct = 1), 1, 0)))/COUNT(answer_id)*100, 2) AS Успешность
FROM subject
     INNER JOIN question ON subject.subject_id = question.subject_id
     INNER JOIN testing ON question.question_id = testing.question_id
GROUP BY name_subject, question.question_id
ORDER BY name_subject ASC, Успешность DESC, Вопрос ASC;
```
































