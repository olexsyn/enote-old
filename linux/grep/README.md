# grep

grep - поиск образца в файле


## Синтаксис

```
/usr/bin/grep [ -bchilnsvw ] ограниченное_регулярное_выражение
    [ имя_файла ... ]
/usr/xpg4/bin/grep [ -E | -F ] [ -c | -l | -q ] [ -bhinsvwx ]
    -e список_образцов ... [ -f файл_образцов ] ...
    [ имя_файла ... ]
/usr/xpg4/bin/grep [ -E | -F ] [ -c | -l | -q ] [ -bhinsvwx ]
    [ -e список_образцов ... ] -f файл_образцов ...
    [ имя_файла ... ]
/usr/xpg4/bin/grep [ -E | -F ] [ -c | -l | -q ] [ -bhinsvwx ]
    образец [ имя_файла ... ]
```


## Описание

Утлита grep выполняет поиск образца в текстовых файлах и выдает все строки, содержащие этот образец. Она использует компактный недетерминированный алгоритм сопоставления.

Будьте внимательны при использовании в списке_образцов символов $, *, [, ^, |, (, ) и \, поскольку они являются метасимволами командного интерпретатора. Лучше брать весь список_образцов в одиночные кавычки '... '.

Если имя_файла не указано, grep предполагает поиск в стандартном входном потоке. Обычно каждая найденная строка копируется в стандартный выходной поток. Если поиск осуществлялся в нескольких файлах, перед каждой найденной строкой выдается имя файла.

## Выводить только определенные строки

Например, строки содержащие `WARN` или `ERROR`

<html>
<pre class="code">
./tail local4.log | <b>grep -v</b> <span style="color:red">-e WARN</span> <span style="color:blue">-e ERROR</span>
</pre>
</html>

## Отрицание в grep

<html>
<pre class="code">
./tail local4.log | <b>grep -v</b> \.pl
</pre>
</html>

множественное отрицание

<html>
<pre class="code">
./tail local4.log | <b>grep -v</b> <span style="color:red">-e mailua\/bin</span> <span style="color:blue">-e Mailua::Storage::DB</span>
</pre>
</html>

(все, кроме строк с ".pl")

Пример, посмотреть стартовавшие fcgi

```
mailua@ans /home/mailua $ ps ax | grep fcgi
 7713 pts/2    S      0:00 /usr/bin/perl /home/mailua/bin/fcgi_manager.pl
 7714 pts/2    S      0:03 /usr/bin/perl /home/mailua/www/mes.fcgi 3
 7726 pts/2    S      0:04 /usr/bin/perl /home/mailua/www/mobile_main.fcgi 5
 7727 pts/2    S      0:07 /usr/bin/perl /home/mailua/www/index.fcgi 6
 7728 pts/2    S      0:04 /usr/bin/perl /home/mailua/www/admin.fcgi 7
 7729 pts/2    S      0:03 /usr/bin/perl /home/mailua/www/cover.fcgi 8
 7730 pts/2    S      0:03 /usr/bin/perl /home/mailua/www/mobile_index.fcgi 10
 7731 pts/2    S      0:01 /usr/bin/perl /home/mailua/www/upl.fcgi 11
 7732 pts/2    S      0:05 /usr/bin/perl /home/mailua/www/cover2.fcgi 12
 7734 pts/2    R      0:05 /usr/bin/perl /home/mailua/www/att.fcgi 13
 7735 pts/2    S      0:03 /usr/bin/perl /home/mailua/www/main.fcgi 15
 7736 pts/2    S      0:04 /usr/bin/perl /home/mailua/www/main.fcgi 15
```

img <http://ans.kiev.ua/wiki/_media/linux/commands/grep.png>
