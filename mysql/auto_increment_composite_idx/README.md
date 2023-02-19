# AUTO_INCREMENT в составном индексе у складовому індексі

В таблицах MyISAM и BDB можно определить AUTO_INCREMENT для вторичного столбца составного ключа. В этом случае значение, генерируемое для автоинкрементного столбца, вычисляется как `MAX(auto_increment_column)+1) WHERE prefix=given-prefix`. Столбец с атрибутом AUTO_INCREMENT удобно использовать, когда данные нужно помещать в упорядоченные группы.

```sql
CREATE TABLE animals (grp ENUM('fish','mammal','bird') NOT NULL,
             id MEDIUMINT NOT NULL AUTO_INCREMENT
             PRIMARY KEY (grp,id));
INSERT INTO animals (grp,name) VALUES("mammal","dog"),("mammal","cat"),
            ("bird","penguin"),("fish","lax"),("mammal","whale");
SELECT * FROM animals ORDER BY grp,id;
```

Что вернет:

```
+--------+----+---------+
| grp    | id | name    |
+--------+----+---------+
| fish   |  1 | lax     |
| mammal |  1 | dog     |
| mammal |  2 | cat     |
| mammal |  3 | whale   |
| bird   |  1 | penguin |
+--------+----+---------+
```

Обратите внимание, что в этом случае значение AUTO_INCREMENT будет использоваться повторно, если в какой-либо группе удаляется строка, содержащая наибольшее значение AUTO_INCREMENT.

Последнее значение поля AUTO_INCREMENT, которое было создано автоматически, можно получить при помощи функции SQL LAST_INSERT_ID() или функции API mysql_insert_id().

Поексперементуємо...

```sql
DROP TABLE IF EXISTS `docid`;
CREATE TABLE `docid` (
`doc_pref` varchar(10) NOT NULL DEFAULT '0',               /* префікс */
`doc_id`   smallint(5) unsigned NOT NULL AUTO_INCREMENT,   /* поле з інкрементом */
`doc_type` smallint(5) unsigned DEFAULT NULL,              /* якесь наступне поле... */ 
...
PRIMARY KEY (`doc_pref`,`doc_id`),                         /* складаний індекс з другим полем doc_id з інкрементом */
) ENGINE=MyISAM;

INSERT INTO `docid` (doc_pref, doc_type, ...) VALUES  # не передаємо doc_id, щоб його генерувала СУБД
('01-01',101,...),  /* '01-01', 1, 101, ... */ 
('01-01',101,...),  /* '01-01', 2, 101, ... */
('01-01',102,...),  /* '01-01', 3, 102, ... */
('01-02',101,...),  /* '01-02', 1, 101, ... */
('01-03',103,...),  /* '01-03', 1, 103, ... */
('01-02',102,...);  /* '01-02', 2, 102, ... */

DELETE FROM docid WHERE doc_pref='01-01' AND doc_id=3;  # видаляємо останній для '01-01'

INSERT INTO `docid` (doc_pref, doc_type, ...) VALUES
('01-01',101,...),  # на місце видаленого запишеться цей зі значенням /* '01-01', 3, 101, ... */
('01-01',102,...);  # /* '01-01', 4, 102, ... */

INSERT INTO `docid` VALUES  # збільшуємо значення інкременту /* '01-01', 10, 102, ... */
('01-01',10,102,...); # вносимо всі значення, разом з AUTO_INCREMENT (10)

INSERT INTO `docid` (doc_pref, doc_type, ...) VALUES # і знову не передаємо doc_id, щоб його генерувала СУБД
('01-01',103,...),  # /* '01-01' ,11, 103,... */
('01-01',104,...);  # /* '01-01', 12, 104,... */
```
