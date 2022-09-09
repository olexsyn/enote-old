# Auto_increment

## Додати AUTO_INCREMENT до ключового поля

    * До уваги! Один із записів таблиці без інкременту мав id = 0. Після додавання до поля id інкременту запис змінив значення id з 0 на max(id)+1. (MariaDB) Логічно, бо інкремент не може мати значення 0.

## Змінити значення AUTO_INCREMENT

```sql
ALTER TABLE tbl_name AUTO_INCREMENT=100
```

## Отримати значення AUTO_INCREMENT


### За допомогою функції MAX()

Але тільки, якщо точно відомо, що значення автоінкременту ніхто не змінював вручну:

```sql
select max(carid)+1 from car;
```
```
+--------------+
| max(carid)+1 |
+--------------+
|          698 |
+--------------+
```

### За допомогою SHOW CREATE TABLE

```sql
SHOW CREATE TABLE car;
```
```
CREATE TABLE `car` (
  `carid` smallint(5) unsigned NOT NULL AUTO_INCREMENT,
  ...
  PRIMARY KEY (`carid`),
) ENGINE=MyISAM AUTO_INCREMENT=698 DEFAULT CHARSET=utf8mb4 |
```

### За допомогою SHOW TABLE STATUS

```sql
SHOW TABLE STATUS FROM `kazkadb` LIKE 'car' \G
```
```
*************************** 1. row ***************************
           Name: car
         Engine: MyISAM
        Version: 10
     Row_format: Dynamic
           Rows: 448
 Avg_row_length: 47
    Data_length: 21304
Max_data_length: 281474976710655
   Index_length: 13312
      Data_free: 0
 Auto_increment: 698
    Create_time: 2021-04-17 22:57:22
    Update_time: 2021-04-17 22:57:22
     Check_time: 2021-04-17 22:57:22
      Collation: utf8mb4_general_ci
       Checksum: NULL
 Create_options: 
        Comment: 
```

### За допомогою INFORMATION_SCHEMA

```sql
SELECT `AUTO_INCREMENT` FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA='kazkadb' AND TABLE_NAME='car';
```
```
+----------------+
| AUTO_INCREMENT |
+----------------+
|            698 |
+----------------+
```
