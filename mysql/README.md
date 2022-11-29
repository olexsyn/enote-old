# MySQL

- [SQLite, MySQL и PostgreSQL: сравниваем популярные реляционные СУБД](sqlite_mysql_postgresql)
- [MariaDB Connector/Python](https://mariadb.com/docs/appdev/connector-python/)
- [MySQL Connector/Python Developer Guide](https://dev.mysql.com/doc/connector-python/en/)
- [Типы данных](datatype)
  - [Про NULL](null)
  - [Datetime или timestamp](https://habr.com/ru/post/61391/)
- [Коректне сортування українських літер](sort_ukr)
- [ALTER TABLE](alter_table)
- [Auto_increment](auto_increment)
- [Клонування таблиць](clone_table)
- [Завантаження даних з файлу](load_data_from_file) - LOAD DATA INFILE
- [LIMIT](limit)
  - [LIMIT з кінця таблиці](limit_from_end)
- [Выборка случайны записей](rand_strings)
- [Как удобно посмотреть данные, когда строка вывода слишком широкая](wide_tables)
- [Права для пользователей. Privileges](privileges)
- [Приклад створення БД та користувача](create_user)
- [Примеры таблиц swimdb](swimdb)
- [Нахождение "дыр" в нумерации](empty_id)
- [Найти записи, которые присутствуют в одной таблице и отсутствуют во второй](missing_values)
- [Выявление и удаление несвязанных записей](unbound_records)

## Добавить столбец с порядковым номером строк в запросе

К сожалению в MySQL нет стандартной функции, которая бы отдавала нам порядковый номер каждой строки. В других базах данных она есть. В ORACLE для этого есть переменная rownum, а в PostgreSQL и msSQL функция ROW_NUMBER().

Пишем свой вариант для MySQL:

```sql
set @n:=0;
Query OK, 0 rows affected (0.000 sec)
select @n:=@n+1 as num, lname, fname, year from prot;
+------+-----------+-----------+------+
| num  | lname     | fname     | year |
+------+-----------+-----------+------+
|    1 | Кот       | Кот       | 2007 |
|    2 | Тка       | Тка       | 2007 |
|    3 | Дор       | Дор       | 2007 |
|    4 | Вла       | Вла       | 2007 |
|    5 | Мел       | Мел       | 2008 |
|    6 | Мал       | Мал       | 2008 |
|    7 | Син       | Син       | 2008 |
|    8 | Оле       | Оле       | 2007 |
|    9 | Бор       | Бор       | 2007 |
|   10 | Рик       | Рик       | 2008 |
...
```
еще: http://www.sql-tutorial.ru/ru/book_row_number_function/page2.html


## Посмотреть все индексы таблицы

```sql
SHOW INDEX FROM table_name;
mysql> show index from rank_st;
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table   | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| rank_st |          0 | PRIMARY  |            1 | id          | A         |         416 |     NULL | NULL   |      | BTREE      |         |               |
| rank_st |          1 | key_main |            1 | course      | A         |           2 |     NULL | NULL   |      | BTREE      |         |               |
| rank_st |          1 | key_main |            2 | gender      | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| rank_st |          1 | key_main |            3 | stroke      | A         |          19 |     NULL | NULL   |      | BTREE      |         |               |
| rank_st |          1 | key_main |            4 | dist        | A         |          69 |     NULL | NULL   |      | BTREE      |         |               |
| rank_st |          1 | key_main |            5 | mstime      | A         |         416 |     NULL | NULL   |      | BTREE      |         |               |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
```

- <http://ans.kiev.ua/wiki/mysql/indexes/choose_index> 
  - <http://ans.kiev.ua/wiki/mysql/btree_hash> BTREE и HASH индексы
  - <http://ans.kiev.ua/wiki/mysql/fulltext0> FULLTEXT
  - <http://ans.kiev.ua/wiki/mysql/fulltext1> FULLTEXT, MATCH/AGAINST
  - <http://ans.kiev.ua/wiki/mysql/fulltext_dubua> Полнотекстовый поиск типа FULLTEXT Дюбуа :book: стр.199-205

- Индексы в MySQL (ruhighload)
- Индексы в MySQL: многоколоночные индексы против комбинированных индексов :habr:
- Основы индексирования и возможности EXPLAIN

---

- Внешние ключи
  - [Внешние ключи](https://metanit.com/sql/mysql/2.5.php)
  - https://pro-prof.com/forums/topic/foreign-key-mysql
  - http://www.mysql.ru/docs/man/ANSI_diff_Foreign_Keys.html - плюсы и минусы
  - http://www.mysql.ru/docs/man/example-Foreign_keys.html - пример
  
- JOIN
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-inner-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-left-join/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-right-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-full-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-self-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-cartesian-ili-cross-joins/
  

- https://andreyex.ru/bazy-dannyx/bd-mysql/vnutrennee-soedinenie-mysql/

- https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-strokovye-funkcii/

- https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-chislovye-funkcii/

https://andreyex.ru/bazy-dannyx/10-rasprostranennyh-oshibok-programmirovaniya-na-sql-i-kak-ih-izbezhat/

https://andreyex.ru/bazy-dannyx/baza-dannyx-mysql/11-osnovnyx-primerov-komandy-update-v-mysql/

https://andreyex.ru/mysql/peremennye-mysql/ + https://andreyex.ru/mysql/peremennaya-select-into-v-mysql/

https://andreyex.ru/mysql/vybor-sluchajnyh-zapisej-v-mysql/

https://andreyex.ru/mysql/kak-sbrasyvat-znacheniya-avtoinkrementa-v-mysql/

https://andreyex.ru/mysql/mariadb-protiv-mysql/


https://andreyex.ru/mysql/kak-sopostavit-znacheniya-null-s-drugimi-znachimymi-znacheniyami/

https://andreyex.ru/mysql/mysql-kommentarii-v-glubinu/




[Как установить PostgreSQL на Ubuntu 20.04](https://andreyex.ru/ubuntu/kak-ustanovit-postgresql-na-ubuntu-20-04/)
