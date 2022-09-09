# LIMIT з кінця таблиці

Робимо підзапит, де вибираємо дані у зворотньому порядку з необхідним лімітом. Потім виводимо дані цієї виборки у необхідному порядку.

```sql
SELECT * FROM ( SELECT id, field1, field2, ...
                FROM tab1 ORDER BY id DESC LIMIT 20 ) AS subquery ORDER BY id;
```

Часто порядок не має значення, а треба лише подивитися останні додані дані. Тоді достатньо такого простого запиту:

```sql
SELECT id, field1, field2, ... FROM tab1 ORDER BY id DESC LIMIT 20;
```
