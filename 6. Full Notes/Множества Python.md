---
created: 2026-07-13T18:07:00
status:
links:
  - "[[Python]]"
  - "[[Переменные Python]]"
  - "[[Типы данных Python]]"
  - "[[Сложные типы данных]]"
---
Неупорядоченная коллекция уникальных элементов.

**Задачи:**
* проверка членства;
* хранение уникальных элементов.

**Свойства:**
* неупорядоченность;
* уникальность;
* изменяемость;
* неизменяемый элементы (только числа, строки, кортежи);
* эффективность.

**Можно добавлять:**

- Числа (int, float, complex)
- Строки (str)
- Кортежи (tuple) с хешируемыми элементами
- Frozenset

**Нельзя добавлять:**

- Списки (list)
- Словари (dict)
- Множества (set)
### Создание множеств

```python
# Множество целых чисел
numbers = {1, 2, 3, 4, 5}
print(numbers)

# Автоматическое удаление дубликатов
duplicates = {1, 2, 2, 3, 3, 3, 4, 5, 5}
print(duplicates)

# Множество с разными типами данных
mixed = {1, "привет", (1, 2, 3)}
print(mixed)
```

#### Конструктор set()
```python
# Пустое множество
empty_set = set()
print(empty_set)

# Создание множества из списка
numbers_set = set([1, 2, 2, 3, 4, 4, 5])
print(numbers_set)

# Создание множества из строки
letters = set("hello")
print(letters)  # 'l' встречается только один раз
```

### Добавление и удаление элементов

```python
fruits = {"яблоко", "банан"}

# Добавление одного элемента
fruits.add("вишня")
print(fruits)

# Добавление нескольких элементов
fruits.update(["груша", "апельсин"])
print(fruits)

# Удаление элемента
fruits.remove("банан")  # вызывает KeyError, если элемента нет
print(fruits)

# Безопасное удаление элемента
fruits.discard("вишня")  # не вызывает ошибку, если элемента нет
print(fruits)

# Извлечение произвольного элемента
random_fruit = fruits.pop()
print(random_fruit)

print(fruits)

# Очистка множества
fruits.clear()
print(fruits)
```

### Математические операции

* **Объединение**
```python
a = {1, 2, 3}
b = {3, 4, 5}

union_set = a | b
print(union_set)
```
* **Пересечение**
```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

intersection_set = a & b
print(intersection_set)
```
* **Разность**
```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

difference_set = a - b
print(difference_set)
```

### Операции сравнения множеств

```python
a = {1, 2, 3}
b = {1, 2, 3, 4, 5}
c = {1, 2, 3}

# Равенство множеств
print(a == c)  # Содержат одинаковые элементы

# Подмножества
print(a.issubset(b))  # Все элементы a есть в b

print(a < b)  # a является строгим подмножеством b

# Надмножества
print(b.issuperset(a))  # b содержит все элементы a

print(b > a)  # b является строгим надмножеством a

# Проверка на отсутствие общих элементов
d = {6, 7, 8}
print(a.isdisjoint(d))  # Нет общих элементов
```

### Неизменяемое множество

```python
immutable_set = frozenset([1, 2, 3, 4])
print(immutable_set)
```

```python
normal_set = {frozenset([1, 2]), frozenset([3, 4])}
print(normal_set)
```

### Примеры

1. Удаление дубликатов из списка
```python
numbers = [1, 2, 2, 3, 3, 3, 4, 5, 5]
unique_numbers = list(set(numbers))
print(unique_numbers)
```

2. Нахождение общих элементов
```python
users_group1 = ["Анна", "Иван", "Мария", "Петр", "Елена"]
users_group2 = ["Иван", "Ольга", "Елена", "Алексей"]

# Общие элементы (пересечение)
common_users = set(users_group1) & set(users_group2)
print(f"Пользователи в обеих группах: {common_users}")

# Элементы только из первой группы (разность)
only_group1 = set(users_group1) - set(users_group2)
print(f"Только в группе 1: {only_group1}")

# Все уникальные элементы (объединение)
all_users = set(users_group1) | set(users_group2)
print(f"Все уникальные пользователи: {all_users}")
```

3. Проверка уникальности элементов
```python
def are_all_unique(items):
    """Проверяет, все ли элементы в последовательности уникальны."""
    return len(set(items)) == len(items)

# True
print(are_all_unique([1, 2, 3, 4, 5]))

# False
print(are_all_unique([1, 2, 3, 3, 4]))
