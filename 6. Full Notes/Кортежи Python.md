---
created: 2026-07-13T16:26:00
status:
links:
  - "[[Python]]"
  - "[[Типы данных Python]]"
  - "[[Сложные типы данных]]"
---
Упорядоченная неизменяемая коллекция. Подходит для данных с фиксированной формой, например координат, RGB-сочетаний и т.д.

Свойства:
* упорядоченность;
* неизменяемость;
* индексируемость;
* допусимость дублиатов;
* включние данных разных типов.

### Создание кортежей

```python
# Пустой кортеж
empty_tuple = ()

# Кортеж с одним элементом (обязательно с запятой!)
single_item = (42,)
print(type(single_item))

# Без запятой будет просто число: (42) == 42
single_item_num = (42)
print(type(single_item_num))

# Кортеж чисел
numbers = (1, 2, 3, 4, 5)

# Кортеж с разными типами данных
mixed = (1, "hello", True, 3.14)

# Вложенные кортежи
nested = ((1, 2), ("a", "b"), (True, False))

# Создание кортежа без скобок
coordinates = 10.5, 20.7, 30.9
print(type(coordinates))

# Создание нового кортежа на основе существующего
new_coordinates = (15.0,) + coordinates[1:]
print(new_coordinates)
```

#### С помощью конструктора tuple()
```python
# Создание пустого кортежа
empty_tuple = tuple()

# Преобразование списка в кортеж
list_to_tuple = tuple([1, 2, 3])
print(list_to_tuple)

# Преобразование строки в кортеж (каждый символ становится элементом)
string_to_tuple = tuple("Python")
print(string_to_tuple)

# Преобразование множества в кортеж
set_to_tuple = tuple({1, 2, 3})
print(set_to_tuple)
```

### Индексация

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")

# Получение элементов по индексу
first_fruit = fruits[0]
print(first_fruit)


# Отрицательные индексы для доступа с конца кортежа
last_fruit = fruits[-1]
print(last_fruit)
```

### Срезы

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")

# Первые три элемента
first_three = fruits[:3]
print(first_three)

# От второго до четвертого
middle = fruits[1:4]
print(middle)

# Разворот кортежа
reversed_tuple = fruits[::-1]
print(reversed_tuple)
```

## Методы

```python
fruits = ("apple", "banana", "cherry", "banana", "date")

# Подсчет количества вхождений элемента
banana_count = fruits.count("banana")
print(banana_count)

# Поиск индекса первого вхождения элемента
banana_index = fruits.index("banana")
print(banana_index)
```

### Операции

```python
# Узнать длину
fruits = ("apple", "banana", "cherry")
print(len(fruits))

# Проверить наличие элемента
print("apple" in fruits)

# Конкатенация (объединение) кортежей
more_fruits = ("pear", "orange")
all_fruits = fruits + more_fruits
print(all_fruits)

# Повторение
repeated = fruits * 2
print(repeated)

# Распаковка
a, b, c = fruits
print(a, b, c)

# Сортировка
people = [("Bob", 30), ("Anna", 25), ("Anna", 30)]
print(sorted(people))
```

### Кортежи vs. Списки

|Характеристика|Список (list)|Кортеж (tuple)|
|---|---|---|
|Синтаксис|[1, 2, 3]|(1, 2, 3)|
|Изменяемость|Да|Нет|
|Методы|Много: append, remove, sort...|Только count, index|
|Производительность|Медленнее|Быстрее|
|Использование памяти|Больше|Меньше|
|Может быть ключом словаря|Нет|Да|
|Подходит для|Коллекций, которые могут меняться|Неизменяемых данных|
