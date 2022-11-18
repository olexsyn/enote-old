# Коректне сортування українських літер

MySQL сортує український алфавіт у такий спосіб: першими йдуть «Є, І, Ї», а потім «А, Б, В».

Щоб не мати проблем з сортуванням, таблиці слід створювати з `CHARACTER SET utf8 COLLATE utf8_unicode_ci`.

Але прочитай це: https://stackoverflow.com/questions/766809/whats-the-difference-between-utf8-general-ci-and-utf8-unicode-ci

Приклад:

```sql
CREATE TABLE test (name CHAR(20) CHARACTER SET utf8 COLLATE utf8_unicode_ci);
```

Тоді:

```
> select name from test;
+------------------+
| name             |
+------------------+
| Петро            |
| Василь           |
| Їбобо            |
| Микола           |
| Єва              |
| Сашко            |
| Івасик           |
| Наталка          |
| Андрійко         |
| Андрєйко         |
| Андрїйко         |
+------------------+

> select name from test order by name;
+------------------+
| name             |
+------------------+
| Андрєйко         |
| Андрійко         |
| Андрїйко         |
| Василь           |
| Єва              |
| Івасик           |
| Їбобо            |
| Микола           |
| Наталка          |
| Петро            |
| Сашко            |
+------------------+

```
