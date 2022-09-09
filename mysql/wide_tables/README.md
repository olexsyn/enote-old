# Как удобно посмотреть данные...

...когда строка вывода слишком широкая

## Вывести данные вертикально

Вместо точки с запятой в конце запроса надо поставить _пробел_ и `\G` (точка с запятой не ставится!):

```sql
select * from user \G"
```

```
*************************** 1. row ***************************
                  Host: localhost
                  User: root
              Password: *9CFBBC772F3Y6C106020035386DA5BBBF1249A11
           Select_priv: Y
           Insert_priv: Y
           Update_priv: Y
           Delete_priv: Y
           Create_priv: Y
             Drop_priv: Y
           Reload_priv: Y
         Shutdown_priv: Y
          Process_priv: Y
             File_priv: Y
            Grant_priv: Y
       References_priv: Y
            Index_priv: Y
            Alter_priv: Y
          Show_db_priv: Y
            Super_priv: Y
 Create_tmp_table_priv: Y
      Lock_tables_priv: Y
          Execute_priv: Y
       Repl_slave_priv: Y
      Repl_client_priv: Y
      Create_view_priv: Y
        Show_view_priv: Y
   Create_routine_priv: Y
    Alter_routine_priv: Y
      Create_user_priv: Y
            Event_priv: Y
          Trigger_priv: Y
Create_tablespace_priv: Y
              ssl_type: 
            ssl_cipher: 
           x509_issuer: 
          x509_subject: 
         max_questions: 0
           max_updates: 0
       max_connections: 0
  max_user_connections: 0
                plugin: unix_socket
 authentication_string: *9CFBBC772F3F6C106020035386DA5BBBF1249A11
      password_expired: N
               is_role: N
          default_role: 
    max_statement_time: 0.000000
*************************** 2. row ***************************
                  Host: localhost
                  User: u_swm
              Password: *C00E70EBF657D13B539EFD50AA8B05D1FD9B5642
           Select_priv: N
           Insert_priv: N
           Update_priv: N
           Delete_priv: N
           Create_priv: N
[...]
```

## Использовать pager

{% include cl.htm
cmd="[mysql]> pager less -S"
out="PAGER set to 'less -S'" %}

{% include cl.htm
cmd="[mysql]> select * from user" %}

Это будет транслировать выход через инструмент командной строки less, который с этим параметром даст табличный вывод, который можно прокручивать по горизонтали и вертикали с помощью клавиш курсора.
Выйти из просмотра можно, нажав клавишу <kbd>Q</kbd>.

{% include cl.htm
cmd="[mysql]> nopager"
out="PAGER set to stdout" %}
