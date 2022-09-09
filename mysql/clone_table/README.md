# Копіювання, клонування таблиць

**Лише структура і ключі вихідної таблиці, без копіювання даних:**

```sql
CREATE TABLE new_table LIKE old_table
```

**Клонувати всю таблицю разом з даними:**

```sql
CREATE TABLE new_table SELECT * FROM old_table
```

**Клонувати всю таблицю, але з умовою:**

```sql
CREATE TABLE new_table LIKE old_table;                     /* створюємо структуру */
INSERT INTO new_table SELECT * FROM old_table WHERE ... ;  /* записуємо дані */
```
