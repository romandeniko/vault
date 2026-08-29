---
created: 2026-07-11T13:22:00
status:
links:
  - "[[Python]]"
---
* Функция без параметров
```python
def greet():
    print("Привет, мир!")
    
greet()
```

* Функция с параметрами
```python
def greet(name):
    print(f"Привет, {name}!")
    
greet("Анна")
```

* Функция с возвращаемым значением
```python
def add(a, b):
    return a + b

# Использование результата функции
result = add(5, 3)
print(f"5 + 3 = {result}")
```

```python
def describe(value):
    if value < 0:
        return "отрицательное"
    return "неотрицательное"
```


#### Параметры функций
```python
# Функция с несколькими параметрами
def describe_pet(animal_type, pet_name):
    print(f"У меня есть {animal_type} по имени {pet_name}.")

# Позиционные аргументы
describe_pet("собака", "Шарик")

# Именованные аргументы
describe_pet(pet_name="Мурка", animal_type="кошка")
```

##### Параметры по умолчанию
```python
# Функция с параметрами по умолчанию
def describe_pet(pet_name, animal_type="собака"):
    print(f"У меня есть {animal_type} по имени {pet_name}.")

# Использование значения по умолчанию
describe_pet("Шарик")

# Переопределение значения по умолчанию
describe_pet("Мурка", "кошка")
```

##### Произвольное кол-во аргументов
```python
def make_pizza(*toppings):
    print("Начинки:", toppings)

make_pizza("пепперони")

make_pizza("грибы", "зеленый перец", "дополнительный сыр")
```

```python
# Произвольное количество именованных аргументов
def build_profile(**user_info):
    print(user_info)

build_profile(name="Анна", location="Москва", field="программирование")
```