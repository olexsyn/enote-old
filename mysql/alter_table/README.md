# ALTER TABLE

Оператор ALTER TABLE обеспечивает возможность изменять структуру существующей таблицы. Например, можно добавлять или удалять столбцы, создавать или уничтожать индексы или переименовывать столбцы либо саму таблицу. Можно также изменять комментарий для таблицы и ее тип.

Оператор ALTER TABLE во время работы создает временную копию исходной таблицы. Требуемое изменение выполняется на копии, затем исходная таблица удаляется, а новая переименовывается.

Например, чтобы **переименовать столбец** INTEGER из a в b, можно сделать следующее:

```sql
ALTER TABLE t1 CHANGE a b INTEGER;
```

Если переименованный столбец был индексируемым - индекс тоже перестроится под новое имя.

При **изменении типа столбца**, но не его имени синтаксис выражения CHANGE все равно требует указания обоих имен столбца, даже если они одинаковы. Например:

```sql
ALTER TABLE t1 CHANGE b b BIGINT NOT NULL;
```

Однако начиная с версии MySQL 3.22.16a можно также использовать выражение MODIFY для **изменения типа столбца без переименовывания** его:

```sql
ALTER TABLE t1 MODIFY b BIGINT NOT NULL;
```

```sql
mysql> desc users;
+--------+------------------+------+-----+------------+----------------+
| Field  | Type             | Null | Key | Default    | Extra          |
+--------+------------------+------+-----+------------+----------------+
| uid    | int(10) unsigned | NO   | PRI | NULL       | auto_increment |
| umail  | varchar(50)      | NO   | UNI | NULL       |                |
| upass  | varchar(100)     | NO   |     | NULL       |                |
| uses   | varchar(50)      | NO   | MUL |            |                |
| ustime | date             | NO   |     | 2012-01-01 |                |
+--------+------------------+------+-----+------------+----------------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE users MODIFY ustime DATETIME NOT NULL DEFAULT "2012-01-01 00:00:00";
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc users;
+--------+------------------+------+-----+---------------------+----------------+
| Field  | Type             | Null | Key | Default             | Extra          |
+--------+------------------+------+-----+---------------------+----------------+
| uid    | int(10) unsigned | NO   | PRI | NULL                | auto_increment |
| umail  | varchar(50)      | NO   | UNI | NULL                |                |
| upass  | varchar(100)     | NO   |     | NULL                |                |
| uses   | varchar(50)      | NO   | MUL |                     |                |
| ustime | datetime         | NO   |     | 2012-01-01 00:00:00 |                |
+--------+------------------+------+-----+---------------------+----------------+
5 rows in set (0.00 sec)
```

## Примеры

Ниже приводятся примеры, показывающие некоторые случаи употребления команды ALTER TABLE. Пример начинается с таблицы t1, которая создается следующим образом:

```sql
CREATE TABLE t1 (a INTEGER,b CHAR(10));
```

Для того чтобы **переименовать таблицу** из t1 в t2:

```sql
ALTER TABLE t1 RENAME t2;
```

Для того чтобы **удалить столбец** c:

```sql
ALTER TABLE t2 DROP COLUMN c;
```

Для того чтобы **добавить новый числовой столбец** AUTO_INCREMENT с именем col:

```sql
ALTER TABLE t2 ADD col INT UNSIGNED NOT NULL AUTO_INCREMENT, ADD INDEX (col);
```

Заметьте, что столбец `col` индексируется (`ADD INDEX`), так как столбцы AUTO_INCREMENT должны быть индексированы, и, кроме того, не могут быть NULL. [Подробнее про NULL](/mysql/null/)

Для того чтобы **изменить тип столбца** ccс INTEGER на TINYINT NOT NULL (оставляя имя прежним) и **изменить тип столбца** bbb сccc CHAR(10) на CHAR(20) **с переименованием** его с bbb на ccc:

```sql
ALTER TABLE t2 MODIFY aaa TINYINT NOT NULL, CHANGE bbb ccc CHAR(20);
```

Для того чтобы **добавить новый столбец** TIMESTAMP с именем ddd **в конец таблицы**:

```sql
ALTER TABLE t2 ADD ddd TIMESTAMP;
```

Вставить новый **столбец** email **после указанного столбца** name:

```sql
ALTER TABLE tab1 ADD email VARCHAR(60) AFTER name;
```

Вставить новый **столбец в начало таблицы**:

```sql
ALTER TABLE tab2 ADD email VARCHAR(60) FIRST;
```

Для того чтобы **добавить индекс к столбцу** ddd и сделать столбец aaa первичным ключом:

```sql
ALTER TABLE t2 ADD INDEX (ddd), ADD PRIMARY KEY (aaa);
```

**создать индексы** к таблице

```sql
ALTER TABLE tmptab ADD FULLTEXT INDEX `idx_goods` (`goods`), ADD INDEX `idx_price` (`price`);
ALTER TABLE swr ADD UNIQUE INDEX uni_name_year (lname, fname, year);
```

**удалить индекс**

```sql
alter table vendor drop index idx_name;
```

```sql
DROP INDEX index_name ON tbl_name
```
подробиці: <https://dev.mysql.com/doc/refman/8.0/en/drop-index.html>

Щоб видалити первинний ключ (а він завжди має ім'я `PRIMARY`) - вкажіть його ім'я у лапках, оскільки `PRIMARY` - це зарезервоване слово:

```sql
DROP INDEX `PRIMARY` ON tab1;
```

### См. также

[Как посмотреть все индексы таблицы](mysql:show_index)

