---
created: 2026-07-15T16:04:00
status:
links:
  - "[[Python]]"
  - "[[Типы данных Python]]"
  - "[[Сложные типы данных]]"
---
Коллекция пар «ключ–значение». Доступ к значению по ключу.

### Создание
```python
# Пустой словарь, который заполним позже
prices = {}

# Словарь сразу с данными
person = {"name": "John", "age": 30, "city": "New York"}
print(person)
```

```python
pairs = [("name", "Anna"), ("age", 28), ("city", "Berlin")]
person = dict(pairs)
print(person)
```

### Чтение
* С помощью квадратных скобок с ключом – если ключа нет, программа остановится ив ернет ошибку. Использовать, есл необходимо найти ошибку/сломанную логику.
```python
person = {"name": "John", "age": 30}
print(person["name"])
```
* С помощью `get()` – если ключа нет, вернет `None`. Использовать, если отсутствие значения – нормальный случай и его необходимо обработать.
```python
person = {"name": "John", "age": 30}

print(person.get("phone"))

print(person.get("phone", "не указан"))
```

### Добавление/изменение значения
```python
person = {"name": "John", "age": 30}

# Ключа "city" не было — он добавляется
person["city"] = "New York"
print(person)

# Ключ "age" уже есть — значение заменяется
person["age"] = 31
print(person)
```

Для нескольких значений использовать `update()`.
```python
person = {"name": "John", "age": 31}
person.update({"age": 32, "job": "developer"})
print(person)
```

### Проверка наличия ключа
```python
person = {"name": "John", "age": 30}

print("name" in person)

print("phone" in person)
```

### Удаление
```python
person = {"name": "John", "age": 30, "job": "developer"}

del person["job"]
print(person)
```

```python
person = {"name": "John", "age": 30}

age = person.pop("age")
print(age)

# Ключа "phone" нет, но второй аргумент спасает от ошибки
phone = person.pop("phone", "не указан")
print(phone)
```

### Перебор
```python
grades = {"John": 90, "Mary": 75, "Kate": 80}

for name in grades:
    print(name, ":", grades[name])
```

```python
grades = {"John": 90, "Mary": 75, "Kate": 80}

for name, grade in grades.items():
    print(name, ":", grade)
```

```python
grades = {"John": 90, "Mary": 75, "Kate": 80}

total = 0
for grade in grades.values():
    total = total + grade
print("Сумма баллов:", total)
```

### Счетчики
```python
text = "one two one two three"
words = text.split()

counts = {}
for word in words:
    if word in counts:
        counts[word] = counts[word] + 1
    else:
        counts[word] = 1
print(counts)
```

```python
text = "one two one two three"
words = text.split()

counts = {}
for word in words:
    counts[word] = counts.get(word, 0) + 1
print(counts)
```

#### Свойства ключей:
* уникальные;
	* неизменяемые (строки, числа, кортежи).