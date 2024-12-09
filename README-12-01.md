# Домашнее задание к занятию «Базы данных» "Важинский ВС"

### Легенда

Заказчик передал вам [файл в формате Excel](https://github.com/netology-code/sdb-homeworks/blob/main/resources/hw-12-1.xlsx), в котором сформирован отчёт. 

На основе этого отчёта нужно выполнить следующие задания.

### Задание 1

Опишите не менее семи таблиц, из которых состоит база данных:

- какие данные хранятся в этих таблицах;
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- ...
- идентификатор структурного подразделения, внешний ключ, integer).

---

### Ответ:

```shell script
region (
 id SERIAL PRIMARY KEY
 region_name VARCHAR(50) NOT NULL 
)

city (
 id SERIAL PRIMARY KEY
 city_name VARCHAR(50)
 region_id INT REFERENCES region(id) NOT NULL 
)

division_type (
 id SERIAL PRIMARY KEY
 division_type_name VARCHAR(50) NOT NULL
)

division_adress (
 id SERIAL PRIMARY KEY
 division_adress VARCHAR(100) NOT NULL
 division_city INT REFERENCES city(id) NOT NULL
)

division (
 id SERIAL PRIMARY KEY
 division_name VARCHAR(50)
 division_type_id INT REFERENCES division_type(id) NOT NULL
 division_adress_id INT REFERENCES division_adress(id) NOT NULL 
)

position (
 id SERIAL PRIMARY KEY
 position_name VARCHAR(100) NOT NULL
 salary INT NOT NULL
)

project (
 id SERIAL PRIMARY KEY
 project_name VARCHAR(50) NOT NULL
)

employee (
 id SERIAL PRIMARY KEY
 first_name VARCHAR(50) NOT NULL
 middle_name VARCHAR(50) NOT NULL
 last_name VARCHAR(50) NOT NULL
 hire_date DATE NOT NULL
 position_id INT REFERENCES position(id) NOT NULL
 division_id INT REFERENCES division(id) NOT NULL
)

project_asignement (
 project_id INT REFERENCES project(id) NOT NULL 
 employee_id INT REFERENCES employee(id) NOT NULL 
)
```
