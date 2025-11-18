---
created: 2025-10-24
status:
links:
  - "[[Базы данных]]"
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Позволяет выбрать n символов из строки слева или справа

```sql
LEFT("abcde", 3) -> "abc"
```

```sql
RIGHT("abcde", 3) -> "abc"
```

```sql
SELECT name_subject, CONCAT(LEFT(name_question, 30), "...") AS Вопрос, COUNT(answer_id) AS Всего_ответов, ROUND(SUM((SELECT IF(answer_id IN (SELECT answer_id FROM answer WHERE is_correct = 1), 1, 0)))/COUNT(answer_id)*100, 2) AS Успешность
FROM subject
     INNER JOIN question ON subject.subject_id = question.subject_id
     INNER JOIN testing ON question.question_id = testing.question_id
GROUP BY name_subject, question.question_id
ORDER BY name_subject ASC, Успешность DESC, Вопрос ASC;
```

```sql
SELECT CONCAT(module.module_id, ' ', LEFT(module_name, 14), '...') AS Модуль, CONCAT(module.module_id, '.', lesson.lesson_position, ' ', LEFT(lesson_name, 12), '...') AS Урок, CONCAT(module.module_id, '.', lesson.lesson_position, '.', step_position, ' ', step_name) AS Шаг
FROM module
     INNER JOIN lesson ON module.module_id = lesson.module_id
     INNER JOIN step ON lesson.lesson_id = step.lesson_id 
WHERE step_name LIKE '%влож%'
ORDER BY module.module_id ASC, lesson_position ASC, step_position ASC;
```
