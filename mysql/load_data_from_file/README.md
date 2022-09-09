# Завантаження даних з файлу

### Помилка mysql: Can't get stat of '/home/user/datafile.txt' (Errcode: 13 "Permission denied")

**MariaDB / (MySQL?)**: Скоріш за все при використанні ```LOAD DATA INFILE ``` ти отримаєш повідомлення про "Permission denied". Ніякі призначення файлу власника "mysql" (як написано далі у статті), або дозволів типу "777" не вплитнуть на результат запиту. Тому що MariaDB  / (MySQL?) за замовчуванням не завантажує файли з директорій користувачів. Читай тут: [MariaDB](https://mariadb.com/kb/en/systemd/#configuring-access-to-home-directories) / ([MySQL](https://dev.mysql.com/doc/refman/8.0/en/load-data.html)).

створюємо директорію (якщо нема):
```
sudo mkdir /etc/systemd/system/mariadb.service.d
```
створюємо в ній файл:
```
sudo tee /etc/systemd/system/mariadb.service.d/dontprotecthome.conf <<EOF
[Service]

ProtectHome=false
EOF
```
Пперезавантажуємо mysql/mariadb...
```
sudo service mysql restart
```

## 10 Примеров входной загрузки данных из текстового файла в таблицы MySQL

https://andreyex.ru/bazy-dannyx/baza-dannyx-mysql/10-primerov-vxodnoj-zagruzki-dannyx-iz-tekstovogo-fajla-v-tablicy-mysql/

Если у вас есть данные в текстовом файле, вы можете легко загрузить их в одну или несколько таблиц в базе данных.

В базе данных MySQL (или MariaDB), используется команда "load data infile" вы можете загрузить данные из текстового файла в таблицы.

Команда загрузки данных из входного файла обеспечивает несколько гибких вариантов для загрузки различных форматов данных из текстового файла в таблицы.

Следующие примеры загрузки данных рассматриваются в данном руководстве:

- Базовый пример для загрузки данных из текстового файла
- Загрузка данных с помощью опции "Fields terminated by"
- Загрузить данные с помощью опции "Enclosed by"
- Использование экранирующего символа в текстовых данных файла
- Загрузить данных с помощью опции "Lines terminated by"
- Игнорировать строки префикса при отправке файлов с помощью опции "Starting By"
- Игнорировать строки заголовка при загрузки файла
- Загрузить только определенные столбцы (и игнорировать другие) при загрузки из файла
- Использование переменной во время загрузки с опцией "Set"
- Написать Shell Скрипт для загрузки данных из текстового файла


### 1. Базовый пример для загрузки данных из текстового файла

В следующем примере файл worker.txt имеет значения полей, которые отделены от вкладки.

```
# cat worker.txt 
100     Andreyex  Sales   5000
200     Boris   IT      5500
300     Anna   IT      7000
400     Anton   Marketing       9500
500     Dima   IT      6000
```

По умолчанию команда загрузки файла данных использует TAB в качестве поля по умолчанию как разделитель.

Во-первых, перейдите в базу данных, куда вы хотите загрузить текстовый файл. В этом примере мы будем загружать вышеуказанный файл worker.txt в таблицу сотрудников, расположенной базе данных MySQL под названием mybase.

```sql
USE mybase;
```

Следующая команда MySQL будет загружать записи из выше указанного файла worker.txt в таблицу сотрудников, как показано ниже. Эта команда не использует никаких дополнительных опций.

```sql
LOAD DATA INFILE 'worker.txt' INTO TABLE employee;
```

Примечание: В приведенном выше примере, команда предполагает, что файл worker.txt находится в директории базы данных. Например, если вы выполняете приведенную выше команду в базу данных mybase, а затем поместите файл в: /var/lib/mysql/mybase/


После загрузки данных, следующее, что мы увидим в таблице сотрудников.

```
MariaDB [mybase]> select * from employee;
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Andreyex | Sales      |   5000 |
| 200 | Boris  | IT |   5500 |
| 300 | Anna  | IT |   7000 |
| 400 | Anton  | Marketing  |   9500 |
| 500 | Dima  | IT |   6000 |
+-----+--------+------------+--------+
```
Примечание: Если вы хотите сделать резервную копию MySQL и восстановить всю базу данных MySQL, используйте команду Mysqldump.


### 2. Выгрузка данных с помощью опции "Fields terminated by"

В следующем примере, во входном файле worker2.txt, значения полей разделяются запятыми.

```
# cat worker2.txt 
100,Andreyex,Sales,5000
200,Boris,IT,5500
300,Anna,IT,7000
400,Anton,Marketing,9500
500,Dima,IT,6000
```

Для того, чтобы загрузить вышеуказанные записи в таблицe сотрудников, используйте следующую команду.

Во время загрузки, используя вариант "FIELDS TERMINATED BY", вы можете указать запятую как разделитель полей, как показано ниже.

```sql
LOAD DATA INFILE 'worker2.txt' 
 INTO TABLE employee 
FIELDS TERMINATED BY ',';
```

Опять же, этот параметр используется только тогда, когда значения поля отделяются друг от друга ничем, кроме TAB. Если поля разделяет двоеточие, вы будете использовать следующую опцию в приведенной выше команде:

```sql
FIELDS TERMINATED BY ':';
```

Если вы новичок в MySQL прочитать: MySQL Учебник: установка, создание БД и таблицы, вставка и выбора записей

Ниже приведены несколько основных ошибок, которые могут произойти во время загрузки MySQL

Ошибка 1: Если текстовый файл не находится под соответствующим каталоге, вы можете получить следующие сообщение об ошибке "ERROR 13 (HY000) Can’t get stat of (Errcode: 2)".

```sql
MariaDB [mybase]> LOAD DATA INFILE 'worker2.txt' INTO TABLE employee;
ERROR 13 (HY000): Can't get stat of '/var/lib/mysql/mybase/worker2.txt' (Errcode: 2)
```

Кроме того, вы можете указать полный путь к файлу в команде при нагрузки данных, как показано ниже. Если вы сделаете это, убедитесь, что файл можно получить по MySQL. Если нет, то измените владельца на MySQL соответствующим образом. Если нет, то вы получите сообщение ошибки в отказе доступа к файлу.

```sql
MariaDB [mybase]> LOAD DATA INFILE '/data/worker2.txt' INTO TABLE employee;
```

Ошибка 2: Если вы не указали правильные поля разделителя, то вы увидите некоторые проблемы в загрузке. В этом примере только первое поле «ID» было загружено. Значение всех остальных полей являются NULL. Это потому, что следующая команда не определяет поле, заканчивающуюся параметром, так как входной файл имел запятую в качестве разделителя поля.

```sql
MariaDB [mybase]> LOAD DATA INFILE 'worker2.txt' INTO TABLE employee;
Query OK, 5 rows affected, 20 warnings (0.00 sec)    
Records: 5  Deleted: 0  Skipped: 0  Warnings: 20

MariaDB [mybase]> select * from employee;
+-----+------+------+--------+
| id  | name | dept | salary |
+-----+------+------+--------+
| 100 | NULL | NULL |   NULL |
| 200 | NULL | NULL |   NULL |
| 300 | NULL | NULL |   NULL |
| 400 | NULL | NULL |   NULL |
| 500 | NULL | NULL |   NULL |
+-----+------+------+--------+
```

### 3. Загрузить данные с помощью опции "Enclosed by"

В следующем примере, текстовый файл имеет значения текстового поля, заключенные в двойные кавычки, т.е. name и department имеют двойные кавычки вокруг них.

```
# cat worker3.txt
100,"Andreyex Smith","Sales & Marketing",5000
200,"Boris Bourne","IT",5500
300,"Anna Jones","IT",7000
400,"Anton Patel","Sales & Marketing",9500
500,"Dima Lee","IT",6000
```

В этом случае используйте вариант "enclosed by", как показано ниже.

```sql
LOAD DATA INFILE 'worker3.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ',' ENCLOSED BY '"';
```

Приведенная выше команда будет загружать записи должным образом, как показано ниже с помощью команды SELECT в mysql:

```sql
MariaDB [mybase]> select * from employee;
+-----+--------------+-------------------+--------+
| id  | name         | dept              | salary |
+-----+--------------+-------------------+--------+
| 100 | Andreyex Smith | Sales & Marketing |   5000 |
| 200 | Boris Bourne | IT        |   5500 |
| 300 | Anna Jones  | IT        |   7000 |
| 400 | Anton Patel  | Sales & Marketing |   9500 |
| 500 | Dima Lee    | IT        |   6000 |
+-----+--------------+-------------------+--------+
```

Обратите внимание, на то что, когда вы объединяете поля с разрывом и поля, заключенные, вы не должны использовать ключевое слово «FIELDS» два раза, как показано ниже, который будет отображаться следующее сообщение об ошибке:

```sql
FIELDS TERMINATED BY ',' FIELDS ENCLOSED BY '"';
```

Выше появится следующая ошибка «ERROR 1064 (42000)«:

ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'FIELDS ENCLOSED BY '"'' at line 4


### 4. Использование экранирующего символа в текстовых данных файла

Допустим, у вас запятая в значении той или иной области.

Например, в следующем примере, имя 2-го поля имеет значение в следующем формате: «Firstname, Lastname«.

```
# cat worker4.txt 
100,Andreyex, Smith,Sales,5000
200,Boris, Bourne,IT,5500
300,Anna, Jones,IT,7000
400,Anton, Patel,Marketing,9500
500,Dima, Lee,IT,6000
```

Если вы загрузите вышеуказанный файл с помощью следующей команды, вы увидите, что он будет отображать «10 предупреждений»

```sql
MariaDB [mybase]> LOAD DATA INFILE 'worker4.txt' 
    ->  INTO TABLE employee 
    ->  FIELDS TERMINATED BY ',';
Query OK, 5 rows affected, 10 warnings (0.00 sec)    
Records: 5  Deleted: 0  Skipped: 0  Warnings: 10
```
Записи также не загружается должным образом, потому что есть запятая в значении одного из полей.

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+---------+--------+
| id  | name   | dept    | salary |
+-----+--------+---------+--------+
| 100 | Andreyex |  Smith  |      0 |
| 200 | Boris  |  Bourne |      0 |
| 300 | Anna  |  Jones  |      0 |
| 400 | Anton  |  Patel  |      0 |
| 500 | Dima  |  Lee    |      0 |
+-----+--------+---------+--------+
```

Правильный файл: Для того, чтобы решить данную проблему, используйте обратную косую черту (\) перед запятой в значении имени поля, как показано ниже.

```
# cat worker4.txt 
100,Andreyex\, Smith,Sales,5000
200,Boris\, Bourne,IT,5500
300,Anna\, Jones,IT,7000
400,Anton\, Patel,Marketing,9500
500,Dima\, Lee,IT,6000
```

Ниже будет работать на этот раз без каких-либо ошибок, так как мы указали \ в качестве экранирующего символа.

```sql
MariaDB [mybase]> LOAD DATA INFILE 'worker4.txt' 
    ->  INTO TABLE employee 
    ->  FIELDS TERMINATED BY ',';

MariaDB [mybase]> select * from employee;
+-----+---------------+------------+--------+
| id  | name          | dept       | salary |
+-----+---------------+------------+--------+
| 100 | Andreyex, Smith | Sales      |   5000 |
| 200 | Boris, Bourne | IT |   5500 |
| 300 | Anna, Jones  | IT |   7000 |
| 400 | Anton, Patel  | Marketing  |   9500 |
| 500 | Dima, Lee    | IT |   6000 |
+-----+---------------+------------+--------+
```

Вы можете также использовать экранирующий символ, как показано ниже. В этом примере мы используем ^ вместо стандартного \.

```
# cat worker41.txt 
100,Andreyex^, Smith,Sales,5000
200,Boris^, Bourne,IT,5500
300,Anna^, Jones,IT,7000
400,Anton^, Patel,Marketing,9500
500,Dima^, Lee,IT,6000
```

В этом случае используйте вариант «ESCAPED BY«, как показано ниже.

```sql
LOAD DATA INFILE 'worker41.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ',' ESCAPED BY '\^'
```

Обратите внимание, что некоторые символы не могут быть использованы в качестве экранирующего символа. Например, если вы используете % в качестве экранирующего символа, вы получите следующее сообщение об ошибке.

```sql
LOAD DATA INFILE 'worker41.txt' 
 INTO TABLE employee 
FIELDS TERMINATED BY ',' ESCAPED BY '\%'

ERROR 1083 (42000): Field separator argument is not what is expected; check the manual
```

### 5. Выгрузка данных с помощью опции "Lines terminated by"

Вместо того, чтобы все записи были указанны на отдельной строке, вы также можете указать их на той же строке.

В следующем примере, каждая запись отделена символом |.

```
# cat worker5.txt 
100,Andreyex,Sales,5000|200,Boris,IT,5500|300,Anna,IT,7000|400,Anton,Marketing,9500|500,Dima,IT,6000
```

Чтобы загрузить вышеуказанный файл, используйте вариант, как показано ниже.

```sql
LOAD DATA INFILE 'worker5.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ','
 LINES TERMINATED BY '|';
```

Приведенная выше команда будет загружать записи из worker5.txt, как показано ниже.

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Andreyex | Sales      |   5000 |
| 200 | Boris  | IT |   5500 |
| 300 | Anna  | IT |   7000 |
| 400 | Anton  | Marketing  |   9500 |
| 500 | Dima  | IT |   6000 |
+-----+--------+------------+--------+
```

Ниже приведены несколько моментов, чтобы иметь в виду:

- Если входной файл поступает из окна, то вы можете использовать эту функцию: LINES TERMINATED BY ‘\r\n’
- Если вы используете CSV файл для загрузки данных в таблицу, то попробуйте одну из этих: 1) LINES TERMINATED BY ‘\r’  2) LINES TERMINATED BY ‘\r\n’

### 6. Игнорировать строки префикса при отправке файлов с помощью опции "Starting By"

Вы также можете иметь некоторый префикс к записям в текстовом файле ввода, который может быть проигнорирован во время загрузки.

Например, в следующем файле worker6.txt, для 1-го, 2-го и 5-й записи, у нас есть «данные:» в начале строки. Вы можете загрузить только эти записи, игнорируя префикс строки.

```
# cat worker6.txt
Data:100,Andreyex,Sales,5000
Data:200,Boris,IT,5500
300,Anna,IT,7000
400,Anton,Marketing,9500
Data:500,Dima,IT,6000
```

Чтобы игнорировать префикс строки и загружать эти записи, (например: «Data:» в приведенном выше файле), используйте опцию "lines starting by", как показано ниже.

```sql
LOAD DATA INFILE 'worker6.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ','
 LINES STARTING BY 'Data:';
```
Ниже приводится выход указанной команды:

```
Query OK, 3 rows affected (0.00 sec)    
Records: 3  Deleted: 0  Skipped: 0  Warnings: 0
```

Как вы видите ниже, выше команда загрузила только записи, созданные с приставкой «Data:«. Это полезно, чтобы выборочно загружать только те записи, которые имеет определенный префикс.

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Andreyex | Sales      |   5000 |
| 200 | Boris  | IT |   5500 |
| 500 | Dima  | IT |   6000 |
+-----+--------+------------+--------+
3 rows in set (0.00 sec)
```

### 7. Игнорировать строки заголовка при загрузки из файла

В следующем входном текстовом файле, первая строка является строкой заголовка, который имеет название столбцов.

```
# cat worker7.txt 
empid,name,department,salary
100,Andreyex,Sales,5000
200,Boris,IT,5500
300,Anna,IT,7000
400,Anton,Marketing,9500
500,Dima,IT,6000
```

Во время загрузки, мы хотим, игнорировать 1-й строку заголовка из файла worker7.txt. Для этого используйте опцию IGNORE 1, как показано ниже.

```sql
LOAD DATA INFILE 'worker7.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ','
 IGNORE 1 LINES;
```

Как видно из следующих выходных данных, даже если входной файл имеет 6 строк, он игнорирует 1-ю линию (которая является строка заголовка) и загрузит оставшиеся 5 строк.

```
Query OK, 5 rows affected (0.00 sec)                 
Records: 5  Deleted: 0  Skipped: 0  Warnings: 0
```

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Andreyex | Sales      |   5000 |
| 200 | Boris  | IT |   5500 |
| 300 | Anna  | IT |   7000 |
| 400 | Anton  | Marketing  |   9500 |
| 500 | Dima  | IT |   6000 |
+-----+--------+------------+--------+
```
### 8. Загрузить только определенные столбцы (и игнорировать другие) при загрузки из файла

В следующем примере мы имеем значения только для трех полей. У нас нет столбца department  в этом примере файла.

```
# cat worker8.txt 
100,Andreyex,5000
200,Boris,5500
300,Anna,7000
400,Anton,9500
500,Dima,6000
```

Для того, чтобы загрузить значения из входной записи на определенный столбец в таблице, укажите имена столбцов во время загрузки данных INFILE, как показано ниже. В последней строке в следующей команде есть имена столбцов, которые должны использоваться для загрузки записей из входного текстового файла.

```sql
LOAD DATA INFILE 'worker8.txt' 
 INTO TABLE employee 
 FIELDS TERMINATED BY ','
 (id, name, salary);
```

Так как мы не указываем колонку «DEPT» в приведенной выше команде, мы увидим, что этот столбец NULL, как показано ниже.

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+------+--------+
| id  | name   | dept | salary |
+-----+--------+------+--------+
| 100 | Andreyex | NULL |   5000 |
| 200 | Boris  | NULL |   5500 |
| 300 | Anna  | NULL |   7000 |
| 400 | Anton  | NULL |   9500 |
| 500 | Dima  | NULL |   6000 |
+-----+--------+------+--------+
```

Опять же, имейте в виду, что, когда вы не указываете список столбцов, то команда будет ожидать, что все столбцы должны присутствовать в файле ввода.

Кроме того, если вы не указали список столбцов в последней строке, вы получите ошибку синтаксиса, как показано ниже.

```sql
MariaDB [mybase]> LOAD DATA INFILE 'worker7.txt' 
    ->  INTO TABLE employee (id, name, salary)
    ->  FIELDS TERMINATED BY ',';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'FIELDS TERMINATED BY ','' at line 3
```

### 9. Использование переменных во время загрузки с опцией «Set»

Для этого примера, давайте использовать следующий файл worker2.txt.

```
# cat worker2.txt 
100,Andreyex,Sales,5000
200,Boris,IT,5500
300,Anna,IT,7000
400,Anton,Marketing,9500
500,Dima,IT,6000
```

В этом примере, мы хотим, увеличить зарплату на 500, прежде чем загружать его в таблицу. Например, заработная плата для Andreyex (является первой записью) 5000. Но, во время загрузки мы хотим увеличить на 500 до 5500, и обновлять это измененное значение в таблице.

Для этого используйте команду SET и использовать зарплату в качестве переменной и сделать приращение, как показано ниже.

```sql
LOAD DATA INFILE 'worker2.txt'
 INTO TABLE employee
 FIELDS TERMINATED BY ','
 (id, name, dept, @salary)
 SET salary = @salary+500;
```

Как видно из следующего вывода, столбец зарплата увеличивается на 500 для всех записей во время загрузки данных из текстового файла.

```sql
MariaDB [mybase]> select * from employee;
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Andreyex | Sales      |   5500 |
| 200 | Boris  | IT |   6000 |
| 300 | Anna  | IT |   7500 |
| 400 | Anton  | Marketing  |  10000 |
| 500 | Dima  | IT |   6500 |
+-----+--------+------------+--------+
```
 
### 10. Запись Shell Скрипт для загрузки данных из текстового файла

Иногда вы можете загрузить данные из текстового файла автоматически, без необходимости входа в MySQL каждый раз.

Скажем, мы хотим поставить следующую команду внутри сценария оболочки и выполнить это автоматически для базе данных mybase.

```sql
LOAD DATA INFILE 'worker2.txt'
 INTO TABLE employee
 FIELDS TERMINATED BY ','
```

Чтобы выполнить загрузку из командной строки, вы можете использовать опцию -e в команде mysql и выполнить его из строки Linux, как показано ниже.

```sql
# mysql -e "LOAD DATA INFILE 'employee2.txt' INTO TABLE employee FIELDS TERMINATED BY ','" \
 -u root -pMySQLPassword mybase
```

Или, вы можете положить, внутри сценария оболочки, как показано ниже. В этом примере сценарий оболочки loads-data.sh имеет указанную выше команду MySQL.

```sql
# cat loads-data.sh 
mysql -e "\
   LOAD DATA INFILE 'worker2.txt'\
    INTO TABLE employee \
	FIELDS TERMINATED BY ','\
	" \
 -u root -pMySQLPwd4MDN! test
```

Дайте разрешение на выполнение на этот скрипт loads-data.sh, и выполните его из командной строки, которая будет загружать данные автоматически в таблицу. Можно также запланировать это как cronjob для загрузки данных из файла автоматически в таблицу на запланированный интервал.

```
# chmod u+x loads-data.sh

# ./loads-data.sh
```
