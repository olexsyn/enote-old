# Приклад створення БД, та користувача

## Вхід

Заходимо під root'ом в MySQL (MariaDB):

Якщо палоль є:

```
sudo mysql -uroot -p
[sudo] password for olex: 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 47
Server version: 10.1.47-MariaDB-0ubuntu0.18.04.1 Ubuntu 18.04
...
```

Якщо система налаштована на вхід без паролю:

```
sudo mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.29-0ubuntu0.22.04.2 (Ubuntu)
...
```

## Створення бази даних

```
CREATE DATABASE db_name;
```
```
CREATE DATABASE IF NOT EXISTS db_name;
```

<https://dev.mysql.com/doc/refman/8.0/en/create-database.html>

<https://mariadb.com/kb/ru/create-database/>

## Переглянути існуючих користувачів та їх привілеї

Список користувачів:

```
SELECT user, host FROM mysql.user;
```

Список привілеїв (для кожного користувача виглядає окремо):

```
SHOW GRANTS FOR 'root'@'localhost';
```

* де `'root'@'localhost'` — обліковий запис, на який дивимося привілеї. Якщо упустити FOR, команда видасть результат користувача, під яким виконано підключення до СУБД.

## Створення користувача та видача прав

Створити користувача без будь-яких прав:

```
CREATE USER 'dbuser'@'localhost' IDENTIFIED BY 'password';
```

**Можемо отримати помилку** про недостатній рівень захищеності пароля:

`ERROR 1819 (HY000): Your password does not satisfy the current policy requirements`

У нових версіях за замовчуванням активовано політику на перевірку складності пароля. Подивимося поточні налаштування:

```
SHOW VARIABLES LIKE 'validate_password%';
+--------------------------------------+--------+
| Variable_name                        | Value  |
+--------------------------------------+--------+
| validate_password.check_user_name    | ON     |
| validate_password.dictionary_file    |        |
| validate_password.length             | 8      |
| validate_password.mixed_case_count   | 1      |
| validate_password.number_count       | 1      |
| validate_password.policy             | MEDIUM |
| validate_password.special_char_count | 1      |
+--------------------------------------+--------+
```

- **validate_password_check_user_name** – пароль не повинен збігатися з ім'ям користувача.
- **validate_password_dictionary_file** - використовувати спеціальний файл із словником заборонених паролів.
- **validate_password_length** – мінімальна довжина пароля.
- **validate_password_mixed_case_count** - скільки, як мінімум, має бути символів у малій та великій розкладках.
- **validate_password_number_count** - яку мінімальну кількість цифр використовувати у паролі.
- **validate_password_policy** – дозволяє задати певний набір правил. Доступні значення LOW (або 0), MEDIUM (1), STRONG (2).
- **validate_password_special_char_count** - мінімальна кількість спеціальних символів (наприклад, # або !).

Можемо змінити деякі параметри:

```
SET GLOBAL validate_password.special_char_count = 0;"
small="Query OK, 0 rows affected (0,02 sec)"
```

Тепер можемо створити користувача з паролем без спеціальних символів.

Після цього права призначаються командою 'GRANT':

```
GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'localhost';
```

До MySQL 8 можна було однією командою і створити користувача, і надати йому права:

`GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;`

Але, починаючи з версії 8, разробники заборонили її використання. Необхідно спочатку створити користувача (CREATE USER).

Опис команди:

- **ALL PRIVILEGES:** надає повні права на використання даних.
- `*.*`: права надаються на всі бази та всі таблиці.
- **dbuser:** ім'я облікового запису.
- **localhost:** доступ до облікового запису буде надано лише з локального комп'ютера.
- **password:** пароль, який буде заданий користувачеві.
- **WITH GRANT OPTION:** будуть надані додаткові права на зміну структури баз та таблиць.

## Інші приклади

**Надання особливих прав користувачу:**

```
GRANT SELECT, UPDATE ON base1.* TO 'dbuser'@'localhost' IDENTIFIED BY 'password';
```

* права на вибірку та оновлення даних у всіх таблицях бази `base1` для користувача `dbuser`
* список всіх можливих прав: all privileges, alter, create, create temporary tables, delete, drop, execute, file, index, insert, lock tables, process, references, reload, replication client, replication slave, select, show databases, shutdown, super, update, usage. [Докладніше](../privileges)

Користувач, що має право змінювати додавати, редагувати, видаляти дані у таблицях однієї бази, створювати тимчасові (для сесії) таблиці:

```
GRANT
  SELECT, UPDATE, INSERT, DELETE, LOCK TABLES, CREATE TEMPORARY TABLES, CREATE VIEW
ON base1.* TO 'dbuser'@'localhost';"
```

Разрешение на удаленное подключение и использование базы MySQL:

```
GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'192.168.0.55' IDENTIFIED BY 'password'
```

предоставит права пользователю `dbuser`, который будет подключаться с компьютера с IP-адресом `192.168.0.55`.

Создание учетной записи MySQL с правами создания резервных копий:

```
GRANT 
  SELECT, SHOW VIEW, RELOAD, REPLICATION CLIENT, EVENT, TRIGGER, LOCK TABLES
ON *.* TO 'backup'@'localhost' IDENTIFIED BY 'backup';
```

## Оновити всі надані привілеї

```
FLUSH PRIVILEGES;
```

Оновити всі привілеї з таблиць привілеїв у базі даних mysql. Якщо сервер запущено з опцією --skip-grant-table, це знову активує таблиці привілеїв.

<https://dev.mysql.com/doc/refman/8.0/en/privilege-changes.html>

<https://mariadb.com/kb/en/flush/>

## Див також

- [Права для пользователей]({{ site.baseurl}}/mysql/privileges)
- {% include a.htm url="https://www.dmosk.ru/miniinstruktions.php?mini=mysql-user" text="Создание пользователей MySQL/MariaDB и предоставление прав доступа" %}
