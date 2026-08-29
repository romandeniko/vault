---
created: 2026-07-23T21:21:00
status:
links:
  - "[[SQL]]"
  - "[[Запросы SQL]]"
---
Основные типы ограничений:

- **PRIMARY KEY** — уникальный идентификатор записи в таблице
```sql
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100)
);
```
ИЛИ
```sql
CREATE TABLE Users (
    id SERIAL,
    username VARCHAR(50),
    email VARCHAR(100),
    CONSTRAINT pk_users PRIMARY KEY (id)
);
```

- **FOREIGN KEY** — обеспечивает ссылочную целостность между таблицами
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    FOREIGN KEY (user_id) REFERENCES Users(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```
Возможные опции для ON DELETE и ON UPDATE:
	- `CASCADE` — автоматически удаляет или обновляет связанные записи
	- `SET NULL` — устанавливает NULL для внешнего ключа
	- `SET DEFAULT` — устанавливает значение по умолчанию
	- `RESTRICT` — запрещает удаление или обновление (используется по умолчанию)
	- `NO ACTION` — аналогично RESTRICT в большинстве СУБД
	
- **UNIQUE** — гарантирует уникальность значений в столбце или группе столбцов
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    email VARCHAR(100) UNIQUE
);
```

- **NOT NULL** — запрещает NULL-значения в столбце
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    bio TEXT
);
```

- **CHECK** — проверяет соответствие данных заданному условию
```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    birth_date DATE NOT NULL,
    hire_date DATE NOT NULL,
    CONSTRAINT chk_dates CHECK (hire_date > birth_date)
);
```

```sql
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(100) CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'),
    age INT CHECK (age >= 0 AND age <= 150)
);
```

- **DEFAULT** — устанавливает значение по умолчанию для столбца
```sql
CREATE TABLE Orders (
    order_id SERIAL PRIMARY KEY,
    user_id INT,
    order_date DATE DEFAULT CURRENT_DATE,
    status VARCHAR(20) DEFAULT 'Pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
```


### Добавление ограничений
```sql
-- Добавление ограничения PRIMARY KEY
ALTER TABLE Users
ADD PRIMARY KEY (id);

-- Добавление ограничения FOREIGN KEY
ALTER TABLE Orders
ADD CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES Users(id);

-- Добавление ограничения UNIQUE
ALTER TABLE Users
ADD CONSTRAINT uq_email UNIQUE (email);

-- Добавление ограничения CHECK
ALTER TABLE Products
ADD CONSTRAINT chk_price CHECK (price > 0);

-- Добавление ограничения NOT NULL
ALTER TABLE Users
ALTER COLUMN username SET NOT NULL;

-- Добавление значения по умолчанию
ALTER TABLE Orders
ALTER COLUMN status SET DEFAULT 'Pending';
```

### Удаление ограничений
```sql
-- Удаление ограничения PRIMARY KEY
ALTER TABLE Users
DROP CONSTRAINT users_pkey;

-- Удаление ограничения FOREIGN KEY
ALTER TABLE Orders
DROP CONSTRAINT fk_user;

-- Удаление ограничения UNIQUE
ALTER TABLE Users
DROP CONSTRAINT uq_email;

-- Удаление ограничения CHECK
ALTER TABLE Products
DROP CONSTRAINT chk_price;

-- Удаление ограничения NOT NULL
ALTER TABLE Users
ALTER COLUMN username DROP NOT NULL;

-- Удаление значения по умолчанию
ALTER TABLE Orders
ALTER COLUMN status DROP DEFAULT;
```






























