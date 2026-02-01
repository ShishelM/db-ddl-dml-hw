# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Рыбянцев Павел`

---

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

![0](/img/image.png)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

![1](/img/image-1.png)

1.6. Переподключитесь к базе данных от имени sys_temp.

![2](/img/image-2.png)

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

![3](/img/image-3.png)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

```sql
-- Создание пользователя, если он не создан переменными окружения
CREATE USER IF NOT EXISTS 'sys_temp'@'%' IDENTIFIED BY 'XXXXXXXX';

-- Выдача всех прав на все базы данных
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

-- Все пользователи
SELECT USER FROM MYSQL.USER;

-- Просмотр прав пользователя sys_temp
SHOW GRANTS FOR 'sys_temp'@'%';

-- Текущий пользователь
SELECT CURRENT_USER;

```


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

```sql
SELECT 
    TABLE_NAME AS 'Название таблицы', 
    COLUMN_NAME AS 'Название первичного ключа'
FROM 
    information_schema.KEY_COLUMN_USAGE
WHERE 
    TABLE_SCHEMA = 'sakila' 
    AND CONSTRAINT_NAME = 'PRIMARY';
```
```
Название таблицы|Название первичного ключа|
----------------+-------------------------+
actor           |actor_id                 |
address         |address_id               |
category        |category_id              |
city            |city_id                  |
country         |country_id               |
customer        |customer_id              |
film            |film_id                  |
film_actor      |actor_id                 |
film_actor      |film_id                  |
film_category   |film_id                  |
film_category   |category_id              |
film_text       |film_id                  |
inventory       |inventory_id             |
language        |language_id              |
payment         |payment_id               |
rental          |rental_id                |
staff           |staff_id                 |
store           |store_id                 |

```
![4](/img/image-4.png)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

```sql
-- Отзыв глобальных прав
REVOKE ALL PRIVILEGES ON *.* FROM 'sys_temp'@'%';

-- Права только на select для бд sakila
GRANT SELECT ON sakila.* TO 'sys_temp'@'%';

-- Обновляю привилегии
FLUSH PRIVILEGES;

```

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

![5](/img/image-5.png)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

